# Optimizing Spark performance<a name="emr-spark-performance"></a>

Amazon EMR provides multiple performance optimization features for Spark\. This topic explains each optimization feature in detail\.

For more information on how to set Spark configuration, see [Configure Spark](emr-spark-configure.md)\.

## Adaptive query execution<a name="emr-spark-performance-aqe"></a>

Adaptive query execution is a framework for reoptimizing query plans based on runtime statistics\. Starting with Amazon EMR 5\.30\.0, the following adaptive query execution optimizations from Apache Spark 3 are available on Apache EMR Runtime for Spark 2\.
+ Adaptive join conversion
+ Adaptive coalescing of shuffle partitions

**Adaptive Join Conversion**

Adaptive join conversion improves query performance by converting sort\-merge\-join operations to broadcast\-hash\-joins operations based on runtime sizes of query stages\. Broadcast\-hash\-joins tend to perform better when one side of the join is small enough to efficiently broadcast its output across all executors, thereby avoiding the need to shuffle exchange and sort both sides of the join\. Adaptive join conversion broadens the range of cases when Spark automatically performs broadcast\-hash\-joins\.

This feature is enabled by default\. It can be disabled by setting `spark.sql.adaptive.enabled` to `false`, which also disables the adaptive query execution framework\. Spark decides to convert a sort\-merge\-join to a broadcast\-hash\-join when the runtime size statistic of one of the join sides does not exceed `spark.sql.autoBroadcastJoinThreshold`, which defaults to 10,485,760 bytes \(10 MiB\)\.

**Adaptive Coalescing of Shuffle Partitions**

Adaptive coalescing of shuffle partitions improves query performance by coalescing small contiguous shuffle partitions to avoid the overhead of having too many small tasks\. This allows you to configure a higher number of initial shuffle partitions upfront that then gets reduced at runtime to a targeted size, improving the chances of having more evenly distributed shuffle partitions\.

This feature is enabled by default unless `spark.sql.shuffle.partitions` is explicitly set\. It can be enabled by setting `spark.sql.adaptive.coalescePartitions.enabled` to `true`\. Both the initial number of shuffle partitions and target partition size can be tuned using the `spark.sql.adaptive.coalescePartitions.minPartitionNum` and `spark.sql.adaptive.advisoryPartitionSizeInBytes` properties respectively\. See the following table for further details on the related Spark properties for this feature\.


**Spark adaptive coalesce partition properties**  

| Property | Default value | Description | 
| --- | --- | --- | 
|  `spark.sql.adaptive.coalescePartitions.enabled`  |  true, unless `spark.sql.shuffle.partitions` is explicitly set  |  When true and spark\.sql\.adaptive\.enabled is true, Spark coalesces contiguous shuffle partitions according to the target size \(specified by `spark.sql.adaptive.advisoryPartitionSizeInBytes`\), to avoid too many small tasks\.  | 
|  `spark.sql.adaptive.advisoryPartitionSizeInBytes`  | 64MB |  The advisory size in bytes of the shuffle partition when coalescing\. This configuration only has an effect when `spark.sql.adaptive.enabled` and `spark.sql.adaptive.coalescePartitions.enabled` are both `true`\.  | 
|  `spark.sql.adaptive.coalescePartitions.minPartitionNum`  | 25 |  The minimum number of shuffle partitions after coalescing\. This configuration only has an effect when `spark.sql.adaptive.enabled` and `spark.sql.adaptive.coalescePartitions.enabled` are both `true`\.  | 
|  `spark.sql.adaptive.coalescePartitions.initialPartitionNum`  | 1000 |  The initial number of shuffle partitions before coalescing\. This configuration only has an effect when `spark.sql.adaptive.enabled` and `spark.sql.adaptive.coalescePartitions.enabled` are both `true`\.  | 

## Dynamic partition pruning<a name="emr-spark-performance-dynamic"></a>

Dynamic partition pruning improves job performance by more accurately selecting the specific partitions within a table that need to be read and processed for a specific query\. By reducing the amount of data read and processed, significant time is saved in job execution\. With Amazon EMR 5\.26\.0, this feature is enabled by default\. With Amazon EMR 5\.24\.0 and 5\.25\.0, you can enable this feature by setting the Spark property `spark.sql.dynamicPartitionPruning.enabled` from within Spark or when creating clusters\. 


**Spark dynamic partition pruning partition properties**  

| Property | Default Value | Description | 
| --- | --- | --- | 
| `spark.sql.dynamicPartitionPruning.enabled` | `true` | When true, enable dynamic partition pruning\. | 
| `spark.sql.optimizer.dynamicPartitionPruning.enforceBroadcastReuse` | `true` | When `true`, Spark performs a defensive check before query execution to ensure that reuse of broadcast exchanges in dynamic pruning filters is not broken by later preparation rules, such as user\-defined columnar rules\. When reuse is broken and this config is `true`, Spark removes the affected dynamic pruning filters to guard against performance and correctness issues\. Correctness issues may arise when the broadcast exchange of the dynamic pruning filter yields different, inconsistent results from the broadcast exchange of the corresponding join operation\. Setting this configuration to `false` should be done with caution; it allows working around scenarios, such as when reuse is broken by user\-defined columnar rules\. When Adaptive Query Execution is enabled, broadcast reuse is always enforced\. | 

This optimization improves upon the existing capabilities of Spark 2\.4\.2, which only supports pushing down static predicates that can be resolved at plan time\.

The following are examples of static predicate push down in Spark 2\.4\.2\.

```
partition_col = 5

partition_col IN (1,3,5)

partition_col between 1 and 3

partition_col = 1 + 3
```

Dynamic partition pruning allows the Spark engine to dynamically infer at runtime which partitions need to be read and which can be safely eliminated\. For example, the following query involves two tables: the `store_sales` table that contains all of the total sales for all stores and is partitioned by region, and the `store_regions` table that contains a mapping of regions for each country\. The tables contain data about stores distributed around the globe, but we are only querying data for North America\.

```
select ss.quarter, ss.region, ss.store, ss.total_sales 
from store_sales ss, store_regions sr
where ss.region = sr.region and sr.country = 'North America'
```

Without dynamic partition pruning, this query will read all regions before filtering out the subset of regions that match the results of the subquery\. With dynamic partition pruning, this query will read and process only the partitions for the regions returned in the subquery\. This saves time and resources by reading less data from storage and processing less records\.

## Flattening scalar subqueries<a name="emr-spark-performance-flatten"></a>

This optimization improves the performance of queries that have scalar subqueries over the same table\. With Amazon EMR 5\.26\.0, this feature is enabled by default\. With Amazon EMR 5\.24\.0 and 5\.25\.0, you can enable it by setting the Spark property `spark.sql.optimizer.flattenScalarSubqueriesWithAggregates.enabled` from within Spark or when creating clusters\. When this property is set to true, the query optimizer flattens aggregate scalar subqueries that use the same relation if possible\. The scalar subqueries are flattened by pushing any predicates present in the subquery into the aggregate functions and then performing one aggregation, with all the aggregate functions, per relation\.

Following is a sample of a query that will benefit from this optimization\.

```
select (select avg(age) from students                    /* Subquery 1 */
                 where age between 5 and 10) as group1,
       (select avg(age) from students                    /* Subquery 2 */
                 where age between 10 and 15) as group2,
       (select avg(age) from students                    /* Subquery 3 */
                 where age between 15 and 20) as group3
```

The optimization rewrites the previous query as:

```
select c1 as group1, c2 as group2, c3 as group3
from (select avg (if(age between 5 and 10, age, null)) as c1,
             avg (if(age between 10 and 15, age, null)) as c2,
             avg (if(age between 15 and 20, age, null)) as c3 from students);
```

Notice that the rewritten query reads the student table only once, and the predicates of the three subqueries are pushed into the `avg` function\.

## DISTINCT before INTERSECT<a name="emr-spark-performance-distinct"></a>

This optimization optimizes joins when using INTERSECT\. With Amazon EMR 5\.26\.0, this feature is enabled by default\. With Amazon EMR 5\.24\.0 and 5\.25\.0, you can enable it by setting the Spark property `spark.sql.optimizer.distinctBeforeIntersect.enabled` from within Spark or when creating clusters\. Queries using INTERSECT are automatically converted to use a left\-semi join\. When this property is set to true, the query optimizer pushes the DISTINCT operator to the children of INTERSECT if it detects that the DISTINCT operator can make the left\-semi join a BroadcastHashJoin instead of a SortMergeJoin\.

Following is a sample of a query that will benefit from this optimization\.

```
(select item.brand brand from store_sales, item
     where store_sales.item_id = item.item_id)
intersect
(select item.brand cs_brand from catalog_sales, item 
     where catalog_sales.item_id = item.item_id)
```

Without enabling this property `spark.sql.optimizer.distinctBeforeIntersect.enabled`, the query will be rewritten as follows\.

```
select distinct brand from
  (select item.brand brand from store_sales, item
     where store_sales.item_id = item.item_id)
left semi join
   (select item.brand cs_brand from catalog_sales, item 
     where catalog_sales.item_id = item.item_id)
 on brand <=> cs_brand
```

When you enable this property `spark.sql.optimizer.distinctBeforeIntersect.enabled`, the query will be rewritten as follows\.

```
select brand from
  (select distinct item.brand brand from store_sales, item
     where store_sales.item_id = item.item_id)
left semi join
   (select distinct item.brand cs_brand from catalog_sales, item 
     where catalog_sales.item_id = item.item_id)
 on brand <=> cs_brand
```

## Bloom filter join<a name="emr-spark-performance-bloom"></a>

This optimization can improve the performance of some joins by pre\-filtering one side of a join using a [Bloom filter](https://en.wikipedia.org/wiki/Bloom_filter) generated from the values from the other side of the join\. With Amazon EMR 5\.26\.0, this feature is enabled by default\. With Amazon EMR 5\.25\.0, you can enable this feature by setting the Spark property `spark.sql.bloomFilterJoin.enabled` to `true` from within Spark or when creating clusters\.

The following is an example query that can benefit from a Bloom filter\.

```
select count(*)
from sales, item
where sales.item_id = item.id
and item.category in (1, 10, 16)
```

When this feature is enabled, the Bloom filter is built from all item ids whose category is in the set of categories being queried\. While scanning the sales table, the Bloom filter is used to determine which sales are for items that are definitely not in the set defined by the Bloom filter\. Thus these identified sales can be filtered out as early as possible\.

## Optimized join reorder<a name="emr-spark-performance-join-reorder"></a>

This optimization can improve query performance by reordering joins involving tables with filters\. With Amazon EMR 5\.26\.0, this feature is enabled by default\. With Amazon EMR 5\.25\.0, you can enable this feature by setting the Spark configuration parameter `spark.sql.optimizer.sizeBasedJoinReorder.enabled` to true\. The default behavior in Spark is to join tables from left to right, as listed in the query\. This strategy can miss opportunities to execute smaller joins with filters first, in order to benefit more expensive joins later\. 

The example query below reports all returned items from all stores in a country\. Without optimized join reorder, Spark joins the two large tables `store_sales` and `store_returns` first, and then joins them with `store` and eventually with `item`\.

```
select ss.item_value, sr.return_date, s.name, i.desc, 
from store_sales ss, store_returns sr, store s, item i
where ss.id = sr.id and ss.store_id = s.id and ss.item_id = i.id
and s.country = 'USA'
```

With optimized join reorder, Spark joins `store_sales` with `store` first since `store` has a filter and is smaller than `store_returns` and `broadcastable`\. Then Spark joins with `store_returns` and finally with `item`\. If `item` had a filter and was broadcastable, it would also qualify for reorder, resulting in `store_sales` joining with `store`, then `item`, and eventually with `store_returns`\.