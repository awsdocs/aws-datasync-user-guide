# DescribeTask<a name="API_DescribeTask"></a>

Returns metadata about a task\.

## Request Syntax<a name="API_DescribeTask_RequestSyntax"></a>

```
{
   "TaskArn": "string"
}
```

## Request Parameters<a name="API_DescribeTask_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [TaskArn](#API_DescribeTask_RequestSyntax) **   <a name="DataSync-DescribeTask-request-TaskArn"></a>
The Amazon Resource Name \(ARN\) of the task to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeTask_ResponseSyntax"></a>

```
{
   "CloudWatchLogGroupArn": "string",
   "CreationTime": number,
   "CurrentTaskExecutionArn": "string",
   "DestinationLocationArn": "string",
   "DestinationNetworkInterfaceArns": [ "string" ],
   "ErrorCode": "string",
   "ErrorDetail": "string",
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
   "SourceNetworkInterfaceArns": [ "string" ],
   "Status": "string",
   "TaskArn": "string"
}
```

## Response Elements<a name="API_DescribeTask_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CloudWatchLogGroupArn](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-CloudWatchLogGroupArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon CloudWatch log group that was used to monitor and log events in the task\.  
For more information on these groups, see [Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch User Guide*\.  
Type: String  
Length Constraints: Maximum length of 562\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):logs:[a-z\-0-9]*:[0-9]{12}:log-group:([^:\*]*)(:\*)?$` 

 ** [CreationTime](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-CreationTime"></a>
The time that the task was created\.  
Type: Timestamp

 ** [CurrentTaskExecutionArn](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-CurrentTaskExecutionArn"></a>
The Amazon Resource Name \(ARN\) of the task execution that is syncing files\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}/execution/exec-[0-9a-f]{17}$` 

 ** [DestinationLocationArn](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-DestinationLocationArn"></a>
The Amazon Resource Name \(ARN\) of the AWS storage resource's location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [DestinationNetworkInterfaceArns](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-DestinationNetworkInterfaceArns"></a>
The Amazon Resource Names \(ARNs\) of the destination elastic network interfaces \(ENIs\) that were created for your subnet\.  
Type: Array of strings  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:aws[\-a-z]{0,}:ec2:[a-z\-0-9]*:[0-9]{12}:network-interface/eni-[0-9a-f]+$` 

 ** [ErrorCode](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-ErrorCode"></a>
Errors that AWS DataSync encountered during execution of the task\. You can use this error code to help troubleshoot issues\.  
Type: String

 ** [ErrorDetail](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-ErrorDetail"></a>
Detailed description of an error that was encountered during the task execution\. You can use this information to help troubleshoot issues\.   
Type: String

 ** [Excludes](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-Excludes"></a>
A list of filter rules that determines which files to exclude from a task\. The list should contain a single filter string that consists of the patterns to exclude\. The patterns are delimited by "\|" \(that is, a pipe\), for example, `"/folder1|/folder2"`\.   
   
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.

 ** [Includes](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-Includes"></a>
A list of filter rules that determines which files to include when running a task\. The pattern contains a single filter string that consists of the patterns to include\. The patterns are delimited by "\|" \(that is, a pipe\), for example, `"/folder1|/folder2`"\.  
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.

 ** [Name](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-Name"></a>
The name of the task that was described\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$` 

 ** [Options](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-Options"></a>
The set of configuration options that control the behavior of a single execution of the task that occurs when you call `StartTaskExecution`\. You can configure these options to preserve metadata such as user ID \(UID\) and group \(GID\), file permissions, data integrity verification, and so on\.  
For each individual task execution, you can override these options by specifying the overriding `OverrideOptions` value to [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html) operation\.   
Type: [Options](API_Options.md) object

 ** [Schedule](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-Schedule"></a>
The schedule used to periodically transfer files from a source to a destination location\.  
Type: [TaskSchedule](API_TaskSchedule.md) object

 ** [SourceLocationArn](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-SourceLocationArn"></a>
The Amazon Resource Name \(ARN\) of the source file system's location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [SourceNetworkInterfaceArns](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-SourceNetworkInterfaceArns"></a>
The Amazon Resource Names \(ARNs\) of the source elastic network interfaces \(ENIs\) that were created for your subnet\.  
Type: Array of strings  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:aws[\-a-z]{0,}:ec2:[a-z\-0-9]*:[0-9]{12}:network-interface/eni-[0-9a-f]+$` 

 ** [Status](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-Status"></a>
The status of the task that was described\.  
For detailed information about task execution statuses, see [Understanding Task Statuses](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-tasks.html#understand-task-creation-statuses) in the * AWS DataSync User Guide\.*   
Type: String  
Valid Values:` AVAILABLE | CREATING | QUEUED | RUNNING | UNAVAILABLE` 

 ** [TaskArn](#API_DescribeTask_ResponseSyntax) **   <a name="DataSync-DescribeTask-response-TaskArn"></a>
The Amazon Resource Name \(ARN\) of the task that was described\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}$` 

## Errors<a name="API_DescribeTask_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeTask_Examples"></a>

### Example<a name="API_DescribeTask_Example_1"></a>

The following example returns information about the task specified in the sample request\.

#### Sample Request<a name="API_DescribeTask_Example_1_Request"></a>

```
{
  "TaskArn": "arn:aws:datasync:us-east-2:111222333444:task/task-08de6e6697796f026"
}
```

### Example<a name="API_DescribeTask_Example_2"></a>

This example illustrates one usage of DescribeTask\.

#### Sample Response<a name="API_DescribeTask_Example_2_Response"></a>

```
{
   "CloudWatchLogGroupArn": "arn:aws:logs:us-east-2:111222333444:log-group"
   "CreationTime": 1532660733.39,
   "CurrentTaskExecutionArn": "arn:aws:datasync:us-east-2:111222333444:task/task-08de6e6697796f026/execution/exec-04ce9d516d69bd52f",
   "Options": { 
      "Atime": "BEST_EFFORT",
      "BytesPerSecond": 1000,
      "Gid": "NONE",
      "Mtime": "PRESERVE",
      "PosixPermissions": "PRESERVE",
      "PreserveDevices": "NONE",
      "PreserveDeletedFiles": "PRESERVE",
      "Uid": "NONE",
      "VerifyMode": "POINT_IN_TIME_CONSISTENT"
   },
   "DestinationLocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50fb",
   "ErrorCode": "???????",
   "ErrorDetail": "??????",
   "Name": "MyTask",
   "SourceLocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50aa",
   "Status": "CREATING",
   "TaskArn": "arn:aws:datasync:us-east-2:111222333444:task/task-08de6e6697796f026"
}
```

## See Also<a name="API_DescribeTask_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeTask) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeTask) 