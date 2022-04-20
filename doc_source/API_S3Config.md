# S3Config<a name="API_S3Config"></a>

The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role used to access an Amazon S3 bucket\.

For detailed information about using such a role, see [Creating a Location for Amazon S3](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html#create-s3-location) in the * AWS DataSync User Guide*\.

## Contents<a name="API_S3Config_Contents"></a>

 ** BucketAccessRoleArn **   <a name="DataSync-Type-S3Config-BucketAccessRoleArn"></a>
The ARN of the IAM role for accessing the S3 bucket\.   
Type: String  
Length Constraints: Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):iam::[0-9]{12}:role/.*$`   
Required: Yes

## See Also<a name="API_S3Config_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/S3Config) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/S3Config) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/S3Config) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/S3Config) 