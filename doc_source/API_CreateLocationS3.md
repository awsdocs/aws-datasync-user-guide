# CreateLocationS3<a name="API_CreateLocationS3"></a>

Creates an endpoint for an Amazon S3 bucket\.

For more information, see [Create an Amazon S3 location](https://docs.aws.amazon.com/datasync/latest/userguide/create-locations-cli.html#create-location-s3-cli) in the * AWS DataSync User Guide*\.

## Request Syntax<a name="API_CreateLocationS3_RequestSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "S3BucketArn": "string",
   "S3Config": { 
      "BucketAccessRoleArn": "string"
   },
   "S3StorageClass": "string",
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationS3_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgentArns](#API_CreateLocationS3_RequestSyntax) **   <a name="DataSync-CreateLocationS3-request-AgentArns"></a>
If you're using DataSync on an AWS Outpost, specify the Amazon Resource Names \(ARNs\) of the DataSync agents deployed on your Outpost\. For more information about launching a DataSync agent on an AWS Outpost, see [Deploy your DataSync agent on AWS Outposts](https://docs.aws.amazon.com/datasync/latest/userguide/deploy-agents.html#outposts-agent)\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: No

 ** [S3BucketArn](#API_CreateLocationS3_RequestSyntax) **   <a name="DataSync-CreateLocationS3-request-S3BucketArn"></a>
The ARN of the Amazon S3 bucket\. If the bucket is on an AWS Outpost, this must be an access point ARN\.  
Type: String  
Length Constraints: Maximum length of 156\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):(s3|s3-outposts):[a-z\-0-9]*:[0-9]*:.*$`   
Required: Yes

 ** [S3Config](#API_CreateLocationS3_RequestSyntax) **   <a name="DataSync-CreateLocationS3-request-S3Config"></a>
The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role used to access an Amazon S3 bucket\.  
For detailed information about using such a role, see [Creating a Location for Amazon S3](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html#create-s3-location) in the * AWS DataSync User Guide*\.  
Type: [S3Config](API_S3Config.md) object  
Required: Yes

 ** [S3StorageClass](#API_CreateLocationS3_RequestSyntax) **   <a name="DataSync-CreateLocationS3-request-S3StorageClass"></a>
The Amazon S3 storage class that you want to store your files in when this location is used as a task destination\. For buckets in AWS Regions, the storage class defaults to Standard\. For buckets on AWS Outposts, the storage class defaults to AWS S3 Outposts\.  
For more information about S3 storage classes, see [Amazon S3 Storage Classes](http://aws.amazon.com/s3/storage-classes/)\. Some storage classes have behaviors that can affect your S3 storage cost\. For detailed information, see [Considerations when working with S3 storage classes in DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes)\.  
Type: String  
Valid Values:` STANDARD | STANDARD_IA | ONEZONE_IA | INTELLIGENT_TIERING | GLACIER | DEEP_ARCHIVE | OUTPOSTS`   
Required: No

 ** [Subdirectory](#API_CreateLocationS3_RequestSyntax) **   <a name="DataSync-CreateLocationS3-request-Subdirectory"></a>
A subdirectory in the Amazon S3 bucket\. This subdirectory in Amazon S3 is used to read data from the S3 source location or write data to the S3 destination\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]*$`   
Required: No

 ** [Tags](#API_CreateLocationS3_RequestSyntax) **   <a name="DataSync-CreateLocationS3-request-Tags"></a>
The key\-value pair that represents the tag that you want to add to the location\. The value can be an empty string\. We recommend using tags to name your resources\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationS3_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationS3_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationS3_ResponseSyntax) **   <a name="DataSync-CreateLocationS3-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the source Amazon S3 bucket location that is created\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationS3_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_CreateLocationS3_Examples"></a>

### Step 1\. Allow to assume the IAM role required to write to the bucket<a name="API_CreateLocationS3_Example_1"></a>

The following example shows the simplest policy that grants the required permissions for AWS DataSync to access a destination Amazon S3 bucket, followed by an IAM role to which the `create-location-s3-iam-role` policy has been attached\.

#### <a name="w142aac37b7c35c17b3b5"></a>

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "datasync.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

#### <a name="w142aac37b7c35c17b3b7"></a>

```
"Role": {
        "Path": "/",
        "RoleName": "MyBucketAccessRole",
        "RoleId": "role-id",
        "Arn": "arn:aws:iam::account-id:role/MyBucketAccessRole",
        "CreateDate": "2018-07-27T02:49:23.117Z",
        "AssumeRolePolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Principal": {
                        "Service": "datasync.amazonaws.com"
                    },
                    "Action": "sts:AssumeRole"
                }
            ]
        }
    }
}
```

### Step 2\. Allow the created IAM role to write to the bucket<a name="API_CreateLocationS3_Example_2"></a>

Attach a policy that has sufficient permissions to access the bucket to the role\. An example of such policy is the `AWSDataSyncFullAccess` managed policy\.

For more information, see [AWSDataSyncFullAccess](https://console.aws.amazon.com/iam/home?#/policies/arn:aws:iam::aws:policy/AWSDataSyncFullAccess$jsonEditor) in the IAM console\.

You don't need to create this policy\. It's managed by AWS, so all that you need to do is specify its ARN in the `attach-role-policy` command\.

#### <a name="w142aac37b7c35c17b5b9"></a>

```
IAM_POLICY_ARN='arn:aws:iam::aws:policy/AWSDataSyncFullAccess'
```

### Step 3\. Create an endpoint for an Amazon S3 bucket<a name="API_CreateLocationS3_Example_3"></a>

The following example creates an endpoint for an Amazon S3 bucket\.

When the S3 endpoint is created, a response similar to the second example following returns the Amazon Resource Name \(ARN\) for the new Amazon S3 location\.

#### Sample Request<a name="API_CreateLocationS3_Example_3_Request"></a>

```
{
  "S3BucketArn": "arn:aws:s3:::MyBucket",
  "S3Config": {
     "BucketAccessRoleArn": "arn:aws:iam::111222333444:role/MyBucketAccessRole",
    },
    "S3StorageClass": "STANDARD",
    "Subdirectory": "/MyFolder",
    "Tags": [
       {
          "Key": "Name",
          "Value": "s3Bucket-1"
       }
     ]
}
```

#### Sample Response<a name="API_CreateLocationS3_Example_3_Response"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50s3"
}
```

## See Also<a name="API_CreateLocationS3_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationS3) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationS3) 