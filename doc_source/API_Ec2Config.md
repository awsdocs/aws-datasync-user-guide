# Ec2Config<a name="API_Ec2Config"></a>

The subnet that AWS DataSync uses to access target EFS file system\. The subnet must have at least one mount target for that file system\. The security group that you provide needs to be able to communicate with the security group on the mount target in the subnet specified\. 

## Contents<a name="API_Ec2Config_Contents"></a>

 ** SecurityGroupArns **   <a name="DataSync-Type-Ec2Config-SecurityGroupArns"></a>
The Amazon Resource Names \(ARNs\) of the security groups that are configured for the Amazon EC2 resource\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: Yes

 ** SubnetArn **   <a name="DataSync-Type-Ec2Config-SubnetArn"></a>
The ARN of the subnet that DataSync uses to access the target EFS file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:subnet/.*$`   
Required: Yes

## See Also<a name="API_Ec2Config_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/Ec2Config) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/Ec2Config) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/Ec2Config) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/Ec2Config) 