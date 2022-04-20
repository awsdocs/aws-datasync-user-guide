# CreateLocationFsxWindows<a name="API_CreateLocationFsxWindows"></a>

Creates an endpoint for an Amazon FSx for Windows File Server file system\.

## Request Syntax<a name="API_CreateLocationFsxWindows_RequestSyntax"></a>

```
{
   "Domain": "string",
   "FsxFilesystemArn": "string",
   "Password": "string",
   "SecurityGroupArns": [ "string" ],
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "User": "string"
}
```

## Request Parameters<a name="API_CreateLocationFsxWindows_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Domain](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-Domain"></a>
The name of the Windows domain that the FSx for Windows File Server belongs to\.  
Type: String  
Length Constraints: Maximum length of 253\.  
Pattern: `^([A-Za-z0-9]+[A-Za-z0-9-.]*)*[A-Za-z0-9-]*[A-Za-z0-9]$`   
Required: No

 ** [FsxFilesystemArn](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-FsxFilesystemArn"></a>
The Amazon Resource Name \(ARN\) for the FSx for Windows File Server file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):fsx:[a-z\-0-9]*:[0-9]{12}:file-system/fs-.*$`   
Required: Yes

 ** [Password](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-Password"></a>
The password of the user who has the permissions to access files and folders in the FSx for Windows File Server file system\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^.{0,104}$`   
Required: Yes

 ** [SecurityGroupArns](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-SecurityGroupArns"></a>
The ARNs of the security groups that are used to configure the FSx for Windows File Server file system\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-Subdirectory"></a>
A subdirectory in the location's path\. This subdirectory in the Amazon FSx for Windows File Server file system is used to read data from the Amazon FSx for Windows File Server source location or write data to the FSx for Windows File Server destination\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: No

 ** [Tags](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-Tags"></a>
The key\-value pair that represents a tag that you want to add to the resource\. The value can be an empty string\. This value helps you manage, filter, and search for your resources\. We recommend that you create a name tag for your location\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

 ** [User](#API_CreateLocationFsxWindows_RequestSyntax) **   <a name="DataSync-CreateLocationFsxWindows-request-User"></a>
The user who has the permissions to access files and folders in the FSx for Windows File Server file system\.  
For information about choosing a user name that ensures sufficient permissions to files, folders, and metadata, see [user](create-fsx-location.html#FSxWuser)\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^[^\x5B\x5D\\/:;|=,+*?]{1,104}$`   
Required: Yes

## Response Syntax<a name="API_CreateLocationFsxWindows_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationFsxWindows_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-CreateLocationFsxWindows-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the FSx for Windows File Server file system location you created\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationFsxWindows_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateLocationFsxWindows_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationFsxWindows) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationFsxWindows) 