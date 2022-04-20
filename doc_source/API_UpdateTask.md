# UpdateTask<a name="API_UpdateTask"></a>

Updates the metadata associated with a task\.

## Request Syntax<a name="API_UpdateTask_RequestSyntax"></a>

```
{
   "CloudWatchLogGroupArn": "string",
   "Excludes": [ 
      { 
         "FilterType": "string",
         "Value": "string"
      }
   ],
   "Includes": [ 
      { 
         "FilterType": "string",
         "Value": "string"
      }
   ],
   "Name": "string",
   "Options": { 
      "Atime": "string",
      "BytesPerSecond": number,
      "Gid": "string",
      "LogLevel": "string",
      "Mtime": "string",
      "OverwriteMode": "string",
      "PosixPermissions": "string",
      "PreserveDeletedFiles": "string",
      "PreserveDevices": "string",
      "SecurityDescriptorCopyFlags": "string",
      "TaskQueueing": "string",
      "TransferMode": "string",
      "Uid": "string",
      "VerifyMode": "string"
   },
   "Schedule": { 
      "ScheduleExpression": "string"
   },
   "TaskArn": "string"
}
```

## Request Parameters<a name="API_UpdateTask_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CloudWatchLogGroupArn](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-CloudWatchLogGroupArn"></a>
The Amazon Resource Name \(ARN\) of the resource name of the Amazon CloudWatch log group\.  
Type: String  
Length Constraints: Maximum length of 562\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):logs:[a-z\-0-9]*:[0-9]{12}:log-group:([^:\*]*)(:\*)?$`   
Required: No

 ** [Excludes](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-Excludes"></a>
A list of filter rules that determines which files to exclude from a task\. The list should contain a single filter string that consists of the patterns to exclude\. The patterns are delimited by "\|" \(that is, a pipe\), for example, `"/folder1|/folder2"`\.  
   
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.  
Required: No

 ** [Includes](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-Includes"></a>
A list of filter rules that determines which files to include when running a task\. The pattern contains a single filter string that consists of the patterns to include\. The patterns are delimited by "\|" \(that is, a pipe\), for example, `"/folder1|/folder2"`\.  
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.  
Required: No

 ** [Name](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-Name"></a>
The name of the task to update\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`   
Required: No

 ** [Options](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-Options"></a>
Represents the options that are available to control the behavior of a [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html) operation\. Behavior includes preserving metadata such as user ID \(UID\), group ID \(GID\), and file permissions, and also overwriting files in the destination, data integrity verification, and so on\.  
A task has a set of default options associated with it\. If you don't specify an option in [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html), the default value is used\. You can override the defaults options on each task execution by specifying an overriding `Options` value to [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html)\.  
Type: [Options](API_Options.md) object  
Required: No

 ** [Schedule](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-Schedule"></a>
Specifies a schedule used to periodically transfer files from a source to a destination location\. You can configure your task to execute hourly, daily, weekly or on specific days of the week\. You control when in the day or hour you want the task to execute\. The time you specify is UTC time\. For more information, see [Scheduling your task](https://docs.aws.amazon.com/datasync/latest/userguide/task-scheduling.html)\.  
Type: [TaskSchedule](API_TaskSchedule.md) object  
Required: No

 ** [TaskArn](#API_UpdateTask_RequestSyntax) **   <a name="DataSync-UpdateTask-request-TaskArn"></a>
The Amazon Resource Name \(ARN\) of the resource name of the task to update\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}$`   
Required: Yes

## Response Elements<a name="API_UpdateTask_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateTask_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateTask_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/UpdateTask) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/UpdateTask) 