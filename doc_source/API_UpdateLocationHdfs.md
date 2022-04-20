# UpdateLocationHdfs<a name="API_UpdateLocationHdfs"></a>

Updates some parameters of a previously created location for a Hadoop Distributed File System cluster\.

## Request Syntax<a name="API_UpdateLocationHdfs_RequestSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "AuthenticationType": "string",
   "BlockSize": number,
   "KerberosKeytab": blob,
   "KerberosKrb5Conf": blob,
   "KerberosPrincipal": "string",
   "KmsKeyProviderUri": "string",
   "LocationArn": "string",
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
   "SimpleUser": "string",
   "Subdirectory": "string"
}
```

## Request Parameters<a name="API_UpdateLocationHdfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgentArns](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-AgentArns"></a>
The ARNs of the agents that are used to connect to the HDFS cluster\.   
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: No

 ** [AuthenticationType](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-AuthenticationType"></a>
The type of authentication used to determine the identity of the user\.   
Type: String  
Valid Values:` SIMPLE | KERBEROS`   
Required: No

 ** [BlockSize](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-BlockSize"></a>
The size of the data blocks to write into the HDFS cluster\.   
Type: Integer  
Valid Range: Minimum value of 1048576\. Maximum value of 1073741824\.  
Required: No

 ** [KerberosKeytab](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-KerberosKeytab"></a>
The Kerberos key table \(keytab\) that contains mappings between the defined Kerberos principal and the encrypted keys\. You can load the keytab from a file by providing the file's address\. If you use the AWS CLI, it performs base64 encoding for you\. Otherwise, provide the base64\-encoded text\.  
Type: Base64\-encoded binary data object  
Length Constraints: Maximum length of 65536\.  
Required: No

 ** [KerberosKrb5Conf](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-KerberosKrb5Conf"></a>
The `krb5.conf` file that contains the Kerberos configuration information\. You can load the `krb5.conf` file by providing the file's address\. If you're using the AWS CLI, it performs the base64 encoding for you\. Otherwise, provide the base64\-encoded text\.  
Type: Base64\-encoded binary data object  
Length Constraints: Maximum length of 131072\.  
Required: No

 ** [KerberosPrincipal](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-KerberosPrincipal"></a>
The Kerberos principal with access to the files and folders on the HDFS cluster\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^.+$`   
Required: No

 ** [KmsKeyProviderUri](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-KmsKeyProviderUri"></a>
The URI of the HDFS cluster's Key Management Server \(KMS\)\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^kms:\/\/http[s]?@(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])(;(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9]))*:[0-9]{1,5}\/kms$`   
Required: No

 ** [LocationArn](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the source HDFS cluster location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

 ** [NameNodes](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-NameNodes"></a>
The NameNode that manages the HDFS namespace\. The NameNode performs operations such as opening, closing, and renaming files and directories\. The NameNode contains the information to map blocks of data to the DataNodes\. You can use only one NameNode\.  
Type: Array of [HdfsNameNode](API_HdfsNameNode.md) objects  
Array Members: Minimum number of 1 item\.  
Required: No

 ** [QopConfiguration](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-QopConfiguration"></a>
The Quality of Protection \(QOP\) configuration specifies the Remote Procedure Call \(RPC\) and data transfer privacy settings configured on the Hadoop Distributed File System \(HDFS\) cluster\.   
Type: [QopConfiguration](API_QopConfiguration.md) object  
Required: No

 ** [ReplicationFactor](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-ReplicationFactor"></a>
The number of DataNodes to replicate the data to when writing to the HDFS cluster\.   
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 512\.  
Required: No

 ** [SimpleUser](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-SimpleUser"></a>
The user name used to identify the client on the host operating system\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[_.A-Za-z0-9][-_.A-Za-z0-9]*$`   
Required: No

 ** [Subdirectory](#API_UpdateLocationHdfs_RequestSyntax) **   <a name="DataSync-UpdateLocationHdfs-request-Subdirectory"></a>
A subdirectory in the HDFS cluster\. This subdirectory is used to read data from or write data to the HDFS cluster\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: No

## Response Elements<a name="API_UpdateLocationHdfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateLocationHdfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateLocationHdfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/UpdateLocationHdfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/UpdateLocationHdfs) 