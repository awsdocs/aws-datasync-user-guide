# Ec2Config<a name="API_Ec2Config"></a>

The subnet and security groups that AWS DataSync uses to access your Amazon EFS file system\.

## Contents<a name="API_Ec2Config_Contents"></a>

 ** SecurityGroupArns **   <a name="DataSync-Type-Ec2Config-SecurityGroupArns"></a>
Specifies the Amazon Resource Names \(ARNs\) of the security groups associated with an Amazon EFS file system's mount target\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: Yes

 ** SubnetArn **   <a name="DataSync-Type-Ec2Config-SubnetArn"></a>
Specifies the ARN of a subnet where DataSync creates the [network interfaces](https://docs.aws.amazon.com/datasync/latest/userguide/datasync-network.html#required-network-interfaces) for managing traffic during your transfer\.  
The subnet must be located:  
+ In the same virtual private cloud \(VPC\) as the Amazon EFS file system\.
+ In the same Availability Zone as at least one mount target for the Amazon EFS file system\.
You don't need to specify a subnet that includes a file system mount target\.
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