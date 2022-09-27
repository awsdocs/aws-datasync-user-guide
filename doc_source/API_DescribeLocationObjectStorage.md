# DescribeLocationObjectStorage<a name="API_DescribeLocationObjectStorage"></a>

Returns metadata about your AWS DataSync location for an object storage system\.

## Request Syntax<a name="API_DescribeLocationObjectStorage_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationObjectStorage_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationObjectStorage_RequestSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the object storage system location that you want information about\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationObjectStorage_ResponseSyntax"></a>

```
{
   "AccessKey": "string",
   "AgentArns": [ "string" ],
   "CreationTime": number,
   "LocationArn": "string",
   "LocationUri": "string",
   "ServerPort": number,
   "ServerProtocol": "string"
}
```

## Response Elements<a name="API_DescribeLocationObjectStorage_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AccessKey](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-AccessKey"></a>
The access key \(for example, a user name\) required to authenticate with the object storage server\.  
Type: String  
Length Constraints: Minimum length of 8\. Maximum length of 200\.  
Pattern: `^.+$` 

 ** [AgentArns](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-AgentArns"></a>
The ARNs of the DataSync agents that can securely connect with your location\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

 ** [CreationTime](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-CreationTime"></a>
The time that the location was created\.  
Type: Timestamp

 ** [LocationArn](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-LocationArn"></a>
The ARN of the object storage system location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-LocationUri"></a>
The URL of the object storage system location\.  
Type: String  
Length Constraints: Maximum length of 4360\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9-]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [ServerPort](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-ServerPort"></a>
The port that your object storage server accepts inbound network traffic on \(for example, port 443\)\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65536\.

 ** [ServerProtocol](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-ServerProtocol"></a>
The protocol that your object storage server uses to communicate\.  
Type: String  
Valid Values:` HTTPS | HTTP` 

## Errors<a name="API_DescribeLocationObjectStorage_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeLocationObjectStorage_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationObjectStorage) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationObjectStorage) 