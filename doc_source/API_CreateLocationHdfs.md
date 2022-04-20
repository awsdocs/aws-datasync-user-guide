# CreateLocationHdfs<a name="API_CreateLocationHdfs"></a>

Creates an endpoint for a Hadoop Distributed File System \(HDFS\)\. 

## Request Syntax<a name="API_CreateLocationHdfs_RequestSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "AuthenticationType": "string",
   "BlockSize": number,
   "KerberosKeytab": blob,
   "KerberosKrb5Conf": blob,
   "KerberosPrincipal": "string",
   "KmsKeyProviderUri": "string",
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
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationHdfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgentArns](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-AgentArns"></a>
The Amazon Resource Names \(ARNs\) of the agents that are used to connect to the HDFS cluster\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: Yes

 ** [AuthenticationType](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-AuthenticationType"></a>
The type of authentication used to determine the identity of the user\.   
Type: String  
Valid Values:` SIMPLE | KERBEROS`   
Required: Yes

 ** [BlockSize](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-BlockSize"></a>
The size of data blocks to write into the HDFS cluster\. The block size must be a multiple of 512 bytes\. The default block size is 128 mebibytes \(MiB\)\.  
Type: Integer  
Valid Range: Minimum value of 1048576\. Maximum value of 1073741824\.  
Required: No

 ** [KerberosKeytab](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-KerberosKeytab"></a>
The Kerberos key table \(keytab\) that contains mappings between the defined Kerberos principal and the encrypted keys\. You can load the keytab from a file by providing the file's address\. If you're using the AWS CLI, it performs base64 encoding for you\. Otherwise, provide the base64\-encoded text\.   
If `KERBEROS` is specified for `AuthenticationType`, this parameter is required\. 
Type: Base64\-encoded binary data object  
Length Constraints: Maximum length of 65536\.  
Required: No

 ** [KerberosKrb5Conf](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-KerberosKrb5Conf"></a>
The `krb5.conf` file that contains the Kerberos configuration information\. You can load the `krb5.conf` file by providing the file's address\. If you're using the AWS CLI, it performs the base64 encoding for you\. Otherwise, provide the base64\-encoded text\.   
If `KERBEROS` is specified for `AuthenticationType`, this parameter is required\.
Type: Base64\-encoded binary data object  
Length Constraints: Maximum length of 131072\.  
Required: No

 ** [KerberosPrincipal](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-KerberosPrincipal"></a>
The Kerberos principal with access to the files and folders on the HDFS cluster\.   
If `KERBEROS` is specified for `AuthenticationType`, this parameter is required\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^.+$`   
Required: No

 ** [KmsKeyProviderUri](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-KmsKeyProviderUri"></a>
The URI of the HDFS cluster's Key Management Server \(KMS\)\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^kms:\/\/http[s]?@(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])(;(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9]))*:[0-9]{1,5}\/kms$`   
Required: No

 ** [NameNodes](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-NameNodes"></a>
The NameNode that manages the HDFS namespace\. The NameNode performs operations such as opening, closing, and renaming files and directories\. The NameNode contains the information to map blocks of data to the DataNodes\. You can use only one NameNode\.  
Type: Array of [HdfsNameNode](API_HdfsNameNode.md) objects  
Array Members: Minimum number of 1 item\.  
Required: Yes

 ** [QopConfiguration](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-QopConfiguration"></a>
The Quality of Protection \(QOP\) configuration specifies the Remote Procedure Call \(RPC\) and data transfer protection settings configured on the Hadoop Distributed File System \(HDFS\) cluster\. If `QopConfiguration` isn't specified, `RpcProtection` and `DataTransferProtection` default to `PRIVACY`\. If you set `RpcProtection` or `DataTransferProtection`, the other parameter assumes the same value\.   
Type: [QopConfiguration](API_QopConfiguration.md) object  
Required: No

 ** [ReplicationFactor](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-ReplicationFactor"></a>
The number of DataNodes to replicate the data to when writing to the HDFS cluster\. By default, data is replicated to three DataNodes\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 512\.  
Required: No

 ** [SimpleUser](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-SimpleUser"></a>
The user name used to identify the client on the host operating system\.   
If `SIMPLE` is specified for `AuthenticationType`, this parameter is required\. 
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[_.A-Za-z0-9][-_.A-Za-z0-9]*$`   
Required: No

 ** [Subdirectory](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-Subdirectory"></a>
A subdirectory in the HDFS cluster\. This subdirectory is used to read data from or write data to the HDFS cluster\. If the subdirectory isn't specified, it will default to `/`\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: No

 ** [Tags](#API_CreateLocationHdfs_RequestSyntax) **   <a name="DataSync-CreateLocationHdfs-request-Tags"></a>
The key\-value pair that represents the tag that you want to add to the location\. The value can be an empty string\. We recommend using tags to name your resources\.   
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationHdfs_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationHdfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationHdfs_ResponseSyntax) **   <a name="DataSync-CreateLocationHdfs-response-LocationArn"></a>
The ARN of the source HDFS cluster location that's created\.   
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationHdfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateLocationHdfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationHdfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationHdfs) 