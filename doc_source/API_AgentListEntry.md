# AgentListEntry<a name="API_AgentListEntry"></a>

Represents a single entry in a list of agents\. `AgentListEntry` returns an array that contains a list of agents when the [ListAgents](https://docs.aws.amazon.com/datasync/latest/userguide/API_ListAgents.html) operation is called\.

## Contents<a name="API_AgentListEntry_Contents"></a>

 ** AgentArn **   <a name="DataSync-Type-AgentListEntry-AgentArn"></a>
The Amazon Resource Name \(ARN\) of the agent\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: No

 ** Name **   <a name="DataSync-Type-AgentListEntry-Name"></a>
The name of the agent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`   
Required: No

 ** Status **   <a name="DataSync-Type-AgentListEntry-Status"></a>
The status of the agent\.  
Type: String  
Valid Values:` ONLINE | OFFLINE`   
Required: No

## See Also<a name="API_AgentListEntry_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/AgentListEntry) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/AgentListEntry) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/AgentListEntry) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/AgentListEntry) 