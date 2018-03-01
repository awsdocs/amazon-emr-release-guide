# Enabling SSL/TLS for Internal Communication Between Nodes<a name="presto-ssl"></a>

With Amazon EMR version 5\.6\.0 and later, you can enable SSL/TLS secured communication between Presto nodes by using a security configuration to enable in\-transit encryption\. For more information, see [Specifying Amazon EMR Encryption Options Using a Security Configuration](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-encryption-enable-security-configuration.html)\. The default port for internal HTTPS is 8446\. The port used for internal communication must be the same port used for HTTPS access to the Presto coordinator\. The `http-server.https.port=port_num` parameter in the Presto `config.properties` file specifies the port\.

When in\-transit encryption is enabled, Amazon EMR does the following for Presto:

+ Distributes the artifacts you specify for in\-transit encryption throughout the Presto cluster\. For more information about encryption artifacts, see [Providing Certificates for In\-Transit Data Encryption](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-encryption-certificates.html)\.

+ Modifies the `config.properties` file for Presto as follows:

  + Sets `http-server.http.enabled=false` on core and task nodes, which disables HTTP in favor of HTTPS\.

  + Sets `http-server.https.*`, `internal-communication.https.*`, and other values to enable HTTPS and specify implementation details, including LDAP parameters if you have enabled and configured LDAP\.