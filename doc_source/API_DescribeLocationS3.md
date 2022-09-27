# DescribeLocationS3<a name="API_DescribeLocationS3"></a>

Returns metadata, such as bucket name, about an Amazon S3 bucket location\.

## Request Syntax<a name="API_DescribeLocationS3_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationS3_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationS3_RequestSyntax) **   <a name="DataSync-DescribeLocationS3-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon S3 bucket location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationS3_ResponseSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "CreationTime": number,
   "LocationArn": "string",
   "LocationUri": "string",
   "S3Config": { 
      "BucketAccessRoleArn": "string"
   },
   "S3StorageClass": "string"
}
```

## Response Elements<a name="API_DescribeLocationS3_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AgentArns](#API_DescribeLocationS3_ResponseSyntax) **   <a name="DataSync-DescribeLocationS3-response-AgentArns"></a>
If you are using DataSync on an AWS Outpost, the Amazon Resource Name \(ARNs\) of the EC2 agents deployed on your Outpost\. For more information about launching a DataSync agent on an AWS Outpost, see [Deploy your DataSync agent on AWS Outposts](https://docs.aws.amazon.com/datasync/latest/userguide/deploy-agents.html#outposts-agent)\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

 ** [CreationTime](#API_DescribeLocationS3_ResponseSyntax) **   <a name="DataSync-DescribeLocationS3-response-CreationTime"></a>
The time that the Amazon S3 bucket location was created\.  
Type: Timestamp

 ** [LocationArn](#API_DescribeLocationS3_ResponseSyntax) **   <a name="DataSync-DescribeLocationS3-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon S3 bucket or access point\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationS3_ResponseSyntax) **   <a name="DataSync-DescribeLocationS3-response-LocationUri"></a>
The URL of the Amazon S3 location that was described\.  
Type: String  
Length Constraints: Maximum length of 4360\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9-]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [S3Config](#API_DescribeLocationS3_ResponseSyntax) **   <a name="DataSync-DescribeLocationS3-response-S3Config"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role used to access an Amazon S3 bucket\.  
For detailed information about using such a role, see [Creating a Location for Amazon S3](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html#create-s3-location) in the * AWS DataSync User Guide*\.  
Type: [S3Config](API_S3Config.md) object

 ** [S3StorageClass](#API_DescribeLocationS3_ResponseSyntax) **   <a name="DataSync-DescribeLocationS3-response-S3StorageClass"></a>
The Amazon S3 storage class that you chose to store your files in when this location is used as a task destination\. For more information about S3 storage classes, see [Amazon S3 Storage Classes](http://aws.amazon.com/s3/storage-classes/)\. Some storage classes have behaviors that can affect your S3 storage cost\. For detailed information, see [Considerations when working with S3 storage classes in DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes)\.  
Type: String  
Valid Values:` STANDARD | STANDARD_IA | ONEZONE_IA | INTELLIGENT_TIERING | GLACIER | DEEP_ARCHIVE | OUTPOSTS` 

## Errors<a name="API_DescribeLocationS3_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeLocationS3_Examples"></a>

### Example<a name="API_DescribeLocationS3_Example_1"></a>

The following example returns information about the S3 location specified in the sample request\.

#### Sample Request<a name="API_DescribeLocationS3_Example_1_Request"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50s3"
}
```

### Example<a name="API_DescribeLocationS3_Example_2"></a>

This example illustrates one usage of DescribeLocationS3\.

#### Sample Response<a name="API_DescribeLocationS3_Example_2_Response"></a>

```
{
   "CreationTime": 1532660733.39,
   "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50s3",
   "LocationUri": "MyBucket.",
   "S3Config": { 
      "BucketAccessRoleArn": "arn:aws:iam::111222333444:role/MyBucketAccessRole",
   }
    "S3StorageClass": "STANDARD"
}
```

## See Also<a name="API_DescribeLocationS3_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationS3) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationS3) 