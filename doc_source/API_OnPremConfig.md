# OnPremConfig<a name="API_OnPremConfig"></a>

A list of Amazon Resource Names \(ARNs\) of agents to use for a Network File System \(NFS\) location\.

## Contents<a name="API_OnPremConfig_Contents"></a>

 ** AgentArns **   <a name="DataSync-Type-OnPremConfig-AgentArns"></a>
ARNs of the agents to use for an NFS location\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: Yes

## See Also<a name="API_OnPremConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/OnPremConfig) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/OnPremConfig) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/OnPremConfig) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/OnPremConfig) 