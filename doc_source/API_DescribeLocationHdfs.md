# DescribeLocationHdfs<a name="API_DescribeLocationHdfs"></a>

Returns metadata, such as the authentication information about the Hadoop Distributed File System \(HDFS\) location\. 

## Request Syntax<a name="API_DescribeLocationHdfs_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationHdfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationHdfs_RequestSyntax) **   <a name="DataSync-DescribeLocationHdfs-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the HDFS cluster location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationHdfs_ResponseSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "AuthenticationType": "string",
   "BlockSize": number,
   "CreationTime": number,
   "KerberosPrincipal": "string",
   "KmsKeyProviderUri": "string",
   "LocationArn": "string",
   "LocationUri": "string",
   "NameNodes": [ 
      { 
         "Hostname": "string",
         "Port": number
      }
   ],
   "QopConfiguration": { 
      "DataTransferProtection": "string",
      "RpcProtection": "string"
   },
   "ReplicationFactor": number,
   "SimpleUser": "string"
}
```

## Response Elements<a name="API_DescribeLocationHdfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AgentArns](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-AgentArns"></a>
The ARNs of the agents that are used to connect to the HDFS cluster\.   
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

 ** [AuthenticationType](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-AuthenticationType"></a>
The type of authentication used to determine the identity of the user\.   
Type: String  
Valid Values:` SIMPLE | KERBEROS` 

 ** [BlockSize](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-BlockSize"></a>
The size of the data blocks to write into the HDFS cluster\.   
Type: Integer  
Valid Range: Minimum value of 1048576\. Maximum value of 1073741824\.

 ** [CreationTime](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-CreationTime"></a>
The time that the HDFS location was created\.  
Type: Timestamp

 ** [KerberosPrincipal](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-KerberosPrincipal"></a>
The Kerberos principal with access to the files and folders on the HDFS cluster\. This parameter is used if the `AuthenticationType` is defined as `KERBEROS`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^.+$` 

 ** [KmsKeyProviderUri](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-KmsKeyProviderUri"></a>
 The URI of the HDFS cluster's Key Management Server \(KMS\)\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^kms:\/\/http[s]?@(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])(;(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9]))*:[0-9]{1,5}\/kms$` 

 ** [LocationArn](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-LocationArn"></a>
The ARN of the HDFS cluster location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-LocationUri"></a>
The URI of the HDFS cluster location\.  
Type: String  
Length Constraints: Maximum length of 4356\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [NameNodes](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-NameNodes"></a>
The NameNode that manage the HDFS namespace\.   
Type: Array of [HdfsNameNode](API_HdfsNameNode.md) objects  
Array Members: Minimum number of 1 item\.

 ** [QopConfiguration](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-QopConfiguration"></a>
The Quality of Protection \(QOP\) configuration specifies the Remote Procedure Call \(RPC\) and data transfer protection settings configured on the Hadoop Distributed File System \(HDFS\) cluster\.   
Type: [QopConfiguration](API_QopConfiguration.md) object

 ** [ReplicationFactor](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-ReplicationFactor"></a>
The number of DataNodes to replicate the data to when writing to the HDFS cluster\.   
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 512\.

 ** [SimpleUser](#API_DescribeLocationHdfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationHdfs-response-SimpleUser"></a>
The user name used to identify the client on the host operating system\. This parameter is used if the `AuthenticationType` is defined as `SIMPLE`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[_.A-Za-z0-9][-_.A-Za-z0-9]*$` 

## Errors<a name="API_DescribeLocationHdfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeLocationHdfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationHdfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationHdfs) 