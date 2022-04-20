# CreateLocationFsxLustre<a name="API_CreateLocationFsxLustre"></a>

Creates an endpoint for an Amazon FSx for Lustre file system\.

## Request Syntax<a name="API_CreateLocationFsxLustre_RequestSyntax"></a>

```
{
   "FsxFilesystemArn": "string",
   "SecurityGroupArns": [ "string" ],
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationFsxLustre_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [FsxFilesystemArn](#API_CreateLocationFsxLustre_RequestSyntax) **   <a name="DataSync-CreateLocationFsxLustre-request-FsxFilesystemArn"></a>
The Amazon Resource Name \(ARN\) for the FSx for Lustre file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):fsx:[a-z\-0-9]*:[0-9]{12}:file-system/fs-.*$`   
Required: Yes

 ** [SecurityGroupArns](#API_CreateLocationFsxLustre_RequestSyntax) **   <a name="DataSync-CreateLocationFsxLustre-request-SecurityGroupArns"></a>
The Amazon Resource Names \(ARNs\) of the security groups that are used to configure the FSx for Lustre file system\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationFsxLustre_RequestSyntax) **   <a name="DataSync-CreateLocationFsxLustre-request-Subdirectory"></a>
A subdirectory in the location's path\. This subdirectory in the FSx for Lustre file system is used to read data from the FSx for Lustre source location or write data to the FSx for Lustre destination\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: No

 ** [Tags](#API_CreateLocationFsxLustre_RequestSyntax) **   <a name="DataSync-CreateLocationFsxLustre-request-Tags"></a>
The key\-value pair that represents a tag that you want to add to the resource\. The value can be an empty string\. This value helps you manage, filter, and search for your resources\. We recommend that you create a name tag for your location\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationFsxLustre_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationFsxLustre_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationFsxLustre_ResponseSyntax) **   <a name="DataSync-CreateLocationFsxLustre-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the FSx for Lustre file system location that's created\.   
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationFsxLustre_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateLocationFsxLustre_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationFsxLustre) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationFsxLustre) 