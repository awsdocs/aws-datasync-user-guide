# PrivateLinkConfig<a name="API_PrivateLinkConfig"></a>

The VPC endpoint, subnet, and security group that an agent uses to access IP addresses in a VPC \(Virtual Private Cloud\)\.

## Contents<a name="API_PrivateLinkConfig_Contents"></a>

 ** PrivateLinkEndpoint **   <a name="DataSync-Type-PrivateLinkConfig-PrivateLinkEndpoint"></a>
The private endpoint that is configured for an agent that has access to IP addresses in a [PrivateLink](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-service.html)\. An agent that is configured with this endpoint will not be accessible over the public internet\.  
Type: String  
Length Constraints: Minimum length of 7\. Maximum length of 15\.  
Pattern: `\A(25[0-5]|2[0-4]\d|[0-1]?\d?\d)(\.(25[0-5]|2[0-4]\d|[0-1]?\d?\d)){3}\z`   
Required: No

 ** SecurityGroupArns **   <a name="DataSync-Type-PrivateLinkConfig-SecurityGroupArns"></a>
The Amazon Resource Names \(ARNs\) of the security groups that are configured for the EC2 resource that hosts an agent activated in a VPC or an agent that has access to a VPC endpoint\.  
Type: Array of strings  
Array Members: Fixed number of 1 item\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: No

 ** SubnetArns **   <a name="DataSync-Type-PrivateLinkConfig-SubnetArns"></a>
The Amazon Resource Names \(ARNs\) of the subnets that are configured for an agent activated in a VPC or an agent that has access to a VPC endpoint\.  
Type: Array of strings  
Array Members: Fixed number of 1 item\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:subnet/.*$`   
Required: No

 ** VpcEndpointId **   <a name="DataSync-Type-PrivateLinkConfig-VpcEndpointId"></a>
The ID of the VPC endpoint that is configured for an agent\. An agent that is configured with a VPC endpoint will not be accessible over the public internet\.  
Type: String  
Pattern: `^vpce-[0-9a-f]{17}$`   
Required: No

## See Also<a name="API_PrivateLinkConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/PrivateLinkConfig) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/PrivateLinkConfig) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/PrivateLinkConfig) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/PrivateLinkConfig) 