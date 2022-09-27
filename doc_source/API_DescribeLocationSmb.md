# DescribeLocationSmb<a name="API_DescribeLocationSmb"></a>

Returns metadata, such as the path and user information about an SMB location\.

## Request Syntax<a name="API_DescribeLocationSmb_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationSmb_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationSmb_RequestSyntax) **   <a name="DataSync-DescribeLocationSmb-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the SMB location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationSmb_ResponseSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "CreationTime": number,
   "Domain": "string",
   "LocationArn": "string",
   "LocationUri": "string",
   "MountOptions": { 
      "Version": "string"
   },
   "User": "string"
}
```

## Response Elements<a name="API_DescribeLocationSmb_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AgentArns](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-AgentArns"></a>
The Amazon Resource Name \(ARN\) of the source SMB file system location that is created\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

 ** [CreationTime](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-CreationTime"></a>
The time that the SMB location was created\.  
Type: Timestamp

 ** [Domain](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-Domain"></a>
The name of the Windows domain that the SMB server belongs to\.  
Type: String  
Length Constraints: Maximum length of 253\.  
Pattern: `^[A-Za-z0-9]((\.|-+)?[A-Za-z0-9]){0,252}$` 

 ** [LocationArn](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the SMB location that was described\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-LocationUri"></a>
The URL of the source SMB location that was described\.  
Type: String  
Length Constraints: Maximum length of 4360\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9-]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [MountOptions](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-MountOptions"></a>
The mount options that are available for DataSync to use to access an SMB location\.  
Type: [SmbMountOptions](API_SmbMountOptions.md) object

 ** [User](#API_DescribeLocationSmb_ResponseSyntax) **   <a name="DataSync-DescribeLocationSmb-response-User"></a>
The user who can mount the share, has the permissions to access files and folders in the SMB share\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^[^\x5B\x5D\\/:;|=,+*?]{1,104}$` 

## Errors<a name="API_DescribeLocationSmb_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeLocationSmb_Examples"></a>

### Example<a name="API_DescribeLocationSmb_Example_1"></a>

This example illustrates one usage of DescribeLocationSmb\.

#### Sample Request<a name="API_DescribeLocationSmb_Example_1_Request"></a>

```
{
  "arn:aws:datasync:us-east-1:111222333444:location/loc-0f01451b140b2af49"
}
```

### Example<a name="API_DescribeLocationSmb_Example_2"></a>

This example illustrates one usage of DescribeLocationSmb\.

#### Sample Response<a name="API_DescribeLocationSmb_Example_2_Response"></a>

```
{
   "AgentArns":[
      "arn:aws:datasync:us-east-2:111222333444:agent/agent-0bc3b3dc9bbc15145",
      "arn:aws:datasync:us-east-2:111222333444:agent/agent-04b3fe3d261a18c8f"
   ],
   "CreationTime":"1532660733.39",
   "Domain":"AMAZON",
   "LocationArn":"arn:aws:datasync:us-east-1:111222333444:location/loc-0f01451b140b2af49",
   "LocationUri":"smb://hostname.amazon.com/share",
   "MountOptions":{
      "Version":"SMB3"
   },
   "User":"user-1"
}
```

## See Also<a name="API_DescribeLocationSmb_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationSmb) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationSmb) 