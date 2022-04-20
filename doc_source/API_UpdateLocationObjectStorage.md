# UpdateLocationObjectStorage<a name="API_UpdateLocationObjectStorage"></a>

Updates some of the parameters of a previously created location for self\-managed object storage server access\. For information about creating a self\-managed object storage location, see [Creating a location for object storage](https://docs.aws.amazon.com/datasync/latest/userguide/create-object-location.html)\.

## Request Syntax<a name="API_UpdateLocationObjectStorage_RequestSyntax"></a>

```
{
   "AccessKey": "string",
   "AgentArns": [ "string" ],
   "LocationArn": "string",
   "SecretKey": "string",
   "ServerPort": number,
   "ServerProtocol": "string",
   "Subdirectory": "string"
}
```

## Request Parameters<a name="API_UpdateLocationObjectStorage_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AccessKey](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-AccessKey"></a>
Optional\. The access key is used if credentials are required to access the self\-managed object storage server\. If your object storage requires a user name and password to authenticate, use `AccessKey` and `SecretKey` to provide the user name and password, respectively\.  
Type: String  
Length Constraints: Minimum length of 8\. Maximum length of 200\.  
Pattern: `^.+$`   
Required: No

 ** [AgentArns](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-AgentArns"></a>
The Amazon Resource Name \(ARN\) of the agents associated with the self\-managed object storage server location\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: No

 ** [LocationArn](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the self\-managed object storage server location to be updated\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

 ** [SecretKey](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-SecretKey"></a>
Optional\. The secret key is used if credentials are required to access the self\-managed object storage server\. If your object storage requires a user name and password to authenticate, use `AccessKey` and `SecretKey` to provide the user name and password, respectively\.  
Type: String  
Length Constraints: Minimum length of 8\. Maximum length of 200\.  
Pattern: `^.+$`   
Required: No

 ** [ServerPort](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-ServerPort"></a>
The port that your self\-managed object storage server accepts inbound network traffic on\. The server port is set by default to TCP 80 \(HTTP\) or TCP 443 \(HTTPS\)\. You can specify a custom port if your self\-managed object storage server requires one\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65536\.  
Required: No

 ** [ServerProtocol](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-ServerProtocol"></a>
The protocol that the object storage server uses to communicate\. Valid values are `HTTP` or `HTTPS`\.  
Type: String  
Valid Values:` HTTPS | HTTP`   
Required: No

 ** [Subdirectory](#API_UpdateLocationObjectStorage_RequestSyntax) **   <a name="DataSync-UpdateLocationObjectStorage-request-Subdirectory"></a>
The subdirectory in the self\-managed object storage server that is used to read data from\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]*$`   
Required: No

## Response Elements<a name="API_UpdateLocationObjectStorage_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateLocationObjectStorage_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateLocationObjectStorage_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/UpdateLocationObjectStorage) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/UpdateLocationObjectStorage) 