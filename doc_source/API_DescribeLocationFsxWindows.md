# DescribeLocationFsxWindows<a name="API_DescribeLocationFsxWindows"></a>

Returns metadata about an Amazon FSx for Windows File Server location, such as information about its path\.

## Request Syntax<a name="API_DescribeLocationFsxWindows_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationFsxWindows_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationFsxWindows_RequestSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the FSx for Windows File Server location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationFsxWindows_ResponseSyntax"></a>

```
{
   "CreationTime": number,
   "Domain": "string",
   "LocationArn": "string",
   "LocationUri": "string",
   "SecurityGroupArns": [ "string" ],
   "User": "string"
}
```

## Response Elements<a name="API_DescribeLocationFsxWindows_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribeLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-response-CreationTime"></a>
The time that the FSx for Windows File Server location was created\.  
Type: Timestamp

 ** [Domain](#API_DescribeLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-response-Domain"></a>
The name of the Windows domain that the FSx for Windows File Server belongs to\.  
Type: String  
Length Constraints: Maximum length of 253\.  
Pattern: `^([A-Za-z0-9]+[A-Za-z0-9-.]*)*[A-Za-z0-9-]*[A-Za-z0-9]$` 

 ** [LocationArn](#API_DescribeLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the FSx for Windows File Server location that was described\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-response-LocationUri"></a>
The URL of the FSx for Windows File Server location that was described\.  
Type: String  
Length Constraints: Maximum length of 4356\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [SecurityGroupArns](#API_DescribeLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-response-SecurityGroupArns"></a>
The Amazon Resource Names \(ARNs\) of the security groups that are configured for the FSx for Windows File Server file system\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$` 

 ** [User](#API_DescribeLocationFsxWindows_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxWindows-response-User"></a>
The user who has the permissions to access files and folders in the FSx for Windows File Server file system\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^[^\x5B\x5D\\/:;|=,+*?]{1,104}$` 

## Errors<a name="API_DescribeLocationFsxWindows_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeLocationFsxWindows_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationFsxWindows) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationFsxWindows) 