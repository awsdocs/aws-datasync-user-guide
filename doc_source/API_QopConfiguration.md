# QopConfiguration<a name="API_QopConfiguration"></a>

The Quality of Protection \(QOP\) configuration specifies the Remote Procedure Call \(RPC\) and data transfer privacy settings configured on the Hadoop Distributed File System \(HDFS\) cluster\.

## Contents<a name="API_QopConfiguration_Contents"></a>

 ** DataTransferProtection **   <a name="DataSync-Type-QopConfiguration-DataTransferProtection"></a>
The data transfer protection setting configured on the HDFS cluster\. This setting corresponds to your `dfs.data.transfer.protection` setting in the `hdfs-site.xml` file on your Hadoop cluster\.  
Type: String  
Valid Values:` DISABLED | AUTHENTICATION | INTEGRITY | PRIVACY`   
Required: No

 ** RpcProtection **   <a name="DataSync-Type-QopConfiguration-RpcProtection"></a>
The RPC protection setting configured on the HDFS cluster\. This setting corresponds to your `hadoop.rpc.protection` setting in your `core-site.xml` file on your Hadoop cluster\.  
Type: String  
Valid Values:` DISABLED | AUTHENTICATION | INTEGRITY | PRIVACY`   
Required: No

## See Also<a name="API_QopConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/QopConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/QopConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/QopConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/QopConfiguration) 