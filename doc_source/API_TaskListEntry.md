# TaskListEntry<a name="API_TaskListEntry"></a>

Represents a single entry in a list of tasks\. `TaskListEntry` returns an array that contains a list of tasks when the [ListTasks](https://docs.aws.amazon.com/datasync/latest/userguide/API_ListTasks.html) operation is called\. A task includes the source and destination file systems to sync and the options to use for the tasks\.

## Contents<a name="API_TaskListEntry_Contents"></a>

 ** Name **   <a name="DataSync-Type-TaskListEntry-Name"></a>
The name of the task\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`   
Required: No

 ** Status **   <a name="DataSync-Type-TaskListEntry-Status"></a>
The status of the task\.  
Type: String  
Valid Values:` AVAILABLE | CREATING | QUEUED | RUNNING | UNAVAILABLE`   
Required: No

 ** TaskArn **   <a name="DataSync-Type-TaskListEntry-TaskArn"></a>
The Amazon Resource Name \(ARN\) of the task\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}$`   
Required: No

## See Also<a name="API_TaskListEntry_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/TaskListEntry) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/TaskListEntry) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/TaskListEntry) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/TaskListEntry) 