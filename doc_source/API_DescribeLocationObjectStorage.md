# DescribeLocationObjectStorage<a name="API_DescribeLocationObjectStorage"></a>

Returns metadata about a self\-managed object storage server location\. For more information about self\-managed object storage locations, see [Creating a location for object storage](https://docs.aws.amazon.com/datasync/latest/userguide/create-object-location.html)\.

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
The Amazon Resource Name \(ARN\) of the self\-managed object storage server location that was described\.  
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
Optional\. The access key is used if credentials are required to access the self\-managed object storage server\. If your object storage requires a user name and password to authenticate, use `AccessKey` and `SecretKey` to provide the user name and password, respectively\.  
Type: String  
Length Constraints: Minimum length of 8\. Maximum length of 200\.  
Pattern: `^.+$` 

 ** [AgentArns](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-AgentArns"></a>
The Amazon Resource Name \(ARN\) of the agents associated with the self\-managed object storage server location\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

 ** [CreationTime](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-CreationTime"></a>
The time that the self\-managed object storage server agent was created\.  
Type: Timestamp

 ** [LocationArn](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the self\-managed object storage server location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-LocationUri"></a>
The URL of the source self\-managed object storage server location that was described\.  
Type: String  
Length Constraints: Maximum length of 4356\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [ServerPort](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-ServerPort"></a>
The port that your self\-managed object storage server accepts inbound network traffic on\. The server port is set by default to TCP 80 \(HTTP\) or TCP 443 \(HTTPS\)\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65536\.

 ** [ServerProtocol](#API_DescribeLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-DescribeLocationObjectStorage-response-ServerProtocol"></a>
The protocol that the object storage server uses to communicate\. Valid values are HTTP or HTTPS\.  
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