# CreateLocationObjectStorage<a name="API_CreateLocationObjectStorage"></a>

Creates an endpoint for an object storage system that AWS DataSync can access for a transfer\. For more information, see [Creating a location for object storage](https://docs.aws.amazon.com/datasync/latest/userguide/create-object-location.html)\.

## Request Syntax<a name="API_CreateLocationObjectStorage_RequestSyntax"></a>

```
{
   "AccessKey": "string",
   "AgentArns": [ "string" ],
   "BucketName": "string",
   "SecretKey": "string",
   "ServerHostname": "string",
   "ServerPort": number,
   "ServerProtocol": "string",
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationObjectStorage_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AccessKey](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-AccessKey"></a>
Specifies the access key \(for example, a user name\) if credentials are required to authenticate with the object storage server\.  
Type: String  
Length Constraints: Minimum length of 8\. Maximum length of 200\.  
Pattern: `^.+$`   
Required: No

 ** [AgentArns](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-AgentArns"></a>
Specifies the Amazon Resource Names \(ARNs\) of the DataSync agents that can securely connect with your location\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: Yes

 ** [BucketName](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-BucketName"></a>
Specifies the name of the object storage bucket involved in the transfer\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 63\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: Yes

 ** [SecretKey](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-SecretKey"></a>
Specifies the secret key \(for example, a password\) if credentials are required to authenticate with the object storage server\.  
Type: String  
Length Constraints: Minimum length of 8\. Maximum length of 200\.  
Pattern: `^.+$`   
Required: No

 ** [ServerHostname](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-ServerHostname"></a>
Specifies the domain name or IP address of the object storage server\. A DataSync agent uses this hostname to mount the object storage server in a network\.  
Type: String  
Length Constraints: Maximum length of 255\.  
Pattern: `^(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])$`   
Required: Yes

 ** [ServerPort](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-ServerPort"></a>
Specifies the port that your object storage server accepts inbound network traffic on \(for example, port 443\)\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65536\.  
Required: No

 ** [ServerProtocol](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-ServerProtocol"></a>
Specifies the protocol that your object storage server uses to communicate\.  
Type: String  
Valid Values:` HTTPS | HTTP`   
Required: No

 ** [Subdirectory](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-Subdirectory"></a>
Specifies the object prefix for your object storage server\. If this is a source location, DataSync only copies objects with this prefix\. If this is a destination location, DataSync writes all objects with this prefix\.   
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]*$`   
Required: No

 ** [Tags](#API_CreateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-CreateLocationObjectStorage-request-Tags"></a>
Specifies the key\-value pair that represents a tag that you want to add to the resource\. Tags can help you manage, filter, and search for your resources\. We recommend creating a name tag for your location\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationObjectStorage_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationObjectStorage_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationObjectStorage_ResponseSyntax) **   <a name="DataSync-CreateLocationObjectStorage-response-LocationArn"></a>
Specifies the ARN of the object storage system location that you create\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationObjectStorage_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateLocationObjectStorage_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationObjectStorage) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationObjectStorage) 