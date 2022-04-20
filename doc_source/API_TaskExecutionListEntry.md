# TaskExecutionListEntry<a name="API_TaskExecutionListEntry"></a>

Represents a single entry in a list of task executions\. `TaskExecutionListEntry` returns an array that contains a list of specific invocations of a task when the [ListTaskExecutions](https://docs.aws.amazon.com/datasync/latest/userguide/API_ListTaskExecutions.html) operation is called\.

## Contents<a name="API_TaskExecutionListEntry_Contents"></a>

 ** Status **   <a name="DataSync-Type-TaskExecutionListEntry-Status"></a>
The status of a task execution\.  
Type: String  
Valid Values:` QUEUED | LAUNCHING | PREPARING | TRANSFERRING | VERIFYING | SUCCESS | ERROR`   
Required: No

 ** TaskExecutionArn **   <a name="DataSync-Type-TaskExecutionListEntry-TaskExecutionArn"></a>
The Amazon Resource Name \(ARN\) of the task that was executed\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}/execution/exec-[0-9a-f]{17}$`   
Required: No

## See Also<a name="API_TaskExecutionListEntry_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/TaskExecutionListEntry) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/TaskExecutionListEntry) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/TaskExecutionListEntry) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/TaskExecutionListEntry) 