# CreateTask<a name="API_CreateTask"></a>

Creates a task\.

A task includes a source location and a destination location, and a configuration that specifies how data is transferred\. A task always transfers data from the source location to the destination location\. The configuration specifies options such as task scheduling, bandwidth limits, etc\. A task is the complete definition of a data transfer\.

When you create a task that transfers data between AWS services in different AWS Regions, one of the two locations that you specify must reside in the Region where DataSync is being used\. The other location must be specified in a different Region\.

You can transfer data between commercial AWS Regions except for China, or between AWS GovCloud \(US\) Regions\.

**Important**  
When you use DataSync to copy files or objects between AWS Regions, you pay for data transfer between Regions\. This is billed as data transfer OUT from your source Region to your destination Region\. For more information, see [Data Transfer pricing](http://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)\. 

## Request Syntax<a name="API_CreateTask_RequestSyntax"></a>

```
{
   "CloudWatchLogGroupArn": "string",
   "DestinationLocationArn": "string",
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
   "SourceLocationArn": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateTask_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CloudWatchLogGroupArn](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-CloudWatchLogGroupArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon CloudWatch log group that is used to monitor and log events in the task\.   
For more information about how to use CloudWatch Logs with DataSync, see [Monitoring Your Task](https://docs.aws.amazon.com/datasync/latest/userguide/monitor-datasync.html#cloudwatchlogs) in the * AWS DataSync User Guide\.*   
For more information about these groups, see [Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch Logs User Guide*\.  
Type: String  
Length Constraints: Maximum length of 562\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):logs:[a-z\-0-9]*:[0-9]{12}:log-group:([^:\*]*)(:\*)?$`   
Required: No

 ** [DestinationLocationArn](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-DestinationLocationArn"></a>
The Amazon Resource Name \(ARN\) of an AWS storage resource's location\.   
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

 ** [Excludes](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-Excludes"></a>
A list of filter rules that determines which files to exclude from a task\. The list should contain a single filter string that consists of the patterns to exclude\. The patterns are delimited by "\|" \(that is, a pipe\), for example, `"/folder1|/folder2"`\.   
   
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.  
Required: No

 ** [Includes](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-Includes"></a>
A list of filter rules that determines which files to include when running a task\. The pattern contains a single filter string that consists of the patterns to include\. The patterns are delimited by "\|" \(that is, a pipe\), for example, `"/folder1|/folder2"`\.  
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.  
Required: No

 ** [Name](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-Name"></a>
The name of a task\. This value is a text reference that is used to identify the task in the console\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`   
Required: No

 ** [Options](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-Options"></a>
The set of configuration options that control the behavior of a single execution of the task that occurs when you call `StartTaskExecution`\. You can configure these options to preserve metadata such as user ID \(UID\) and group ID \(GID\), file permissions, data integrity verification, and so on\.  
For each individual task execution, you can override these options by specifying the `OverrideOptions` before starting the task execution\. For more information, see the [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html) operation\.   
Type: [Options](API_Options.md) object  
Required: No

 ** [Schedule](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-Schedule"></a>
Specifies a schedule used to periodically transfer files from a source to a destination location\. The schedule should be specified in UTC time\. For more information, see [Scheduling your task](https://docs.aws.amazon.com/datasync/latest/userguide/task-scheduling.html)\.  
Type: [TaskSchedule](API_TaskSchedule.md) object  
Required: No

 ** [SourceLocationArn](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-SourceLocationArn"></a>
The Amazon Resource Name \(ARN\) of the source location for the task\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

 ** [Tags](#API_CreateTask_RequestSyntax) **   <a name="DataSync-CreateTask-request-Tags"></a>
The key\-value pair that represents the tag that you want to add to the resource\. The value can be an empty string\.   
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateTask_ResponseSyntax"></a>

```
{
   "TaskArn": "string"
}
```

## Response Elements<a name="API_CreateTask_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [TaskArn](#API_CreateTask_ResponseSyntax) **   <a name="DataSync-CreateTask-response-TaskArn"></a>
The Amazon Resource Name \(ARN\) of the task\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}$` 

## Errors<a name="API_CreateTask_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_CreateTask_Examples"></a>

### Example<a name="API_CreateTask_Example_1"></a>

The following example creates a task using a source and destination locations\.

#### Sample Request<a name="API_CreateTask_Example_1_Request"></a>

```
{
  "Options": { 
      "Atime": "BEST_EFFORT",
      "Gid": "NONE",
      "Mtime": "PRESERVE",
      "PosixPermissions": "PRESERVE",
      "PreserveDevices": "NONE",
      "PreserveDeletedFiles": "PRESERVE",
      "Uid": "NONE",
      "VerifyMode": "POINT_IN_TIME_CONSISTENT",
   },
   "Schedule": { 
      "ScheduleExpression": "0 12 ? * SUN,WED *"
   },
    "CloudWatchLogGroupArn": "arn:aws:logs:us-east-2:111222333444:log-group",
   "DestinationLocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50fb",
   "Name": "MyTask",
   "SourceLocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-0f01451b140b2af49",
   "Tags": [ 
       { 
          "Key": "Name",
          "Value": "Task-1"
       }
    ]
}
```

### Example<a name="API_CreateTask_Example_2"></a>

The following response returns the Amazon Resource Name \(ARN\) of the task\.

#### Sample Response<a name="API_CreateTask_Example_2_Response"></a>

```
{
  "TaskArn": "arn:aws:datasync:us-east-2:111222333444:task/task-08de6e6697796f026"
}
```

## See Also<a name="API_CreateTask_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateTask) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateTask) 