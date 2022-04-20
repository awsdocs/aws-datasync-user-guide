# DescribeTaskExecution<a name="API_DescribeTaskExecution"></a>

Returns detailed metadata about a task that is being executed\.

## Request Syntax<a name="API_DescribeTaskExecution_RequestSyntax"></a>

```
{
   "TaskExecutionArn": "string"
}
```

## Request Parameters<a name="API_DescribeTaskExecution_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [TaskExecutionArn](#API_DescribeTaskExecution_RequestSyntax) **   <a name="DataSync-DescribeTaskExecution-request-TaskExecutionArn"></a>
The Amazon Resource Name \(ARN\) of the task that is being executed\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}/execution/exec-[0-9a-f]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeTaskExecution_ResponseSyntax"></a>

```
{
   "BytesTransferred": number,
   "BytesWritten": number,
   "EstimatedBytesToTransfer": number,
   "EstimatedFilesToTransfer": number,
   "Excludes": [ 
      { 
         "FilterType": "string",
         "Value": "string"
      }
   ],
   "FilesTransferred": number,
   "Includes": [ 
      { 
         "FilterType": "string",
         "Value": "string"
      }
   ],
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
   "Result": { 
      "ErrorCode": "string",
      "ErrorDetail": "string",
      "PrepareDuration": number,
      "PrepareStatus": "string",
      "TotalDuration": number,
      "TransferDuration": number,
      "TransferStatus": "string",
      "VerifyDuration": number,
      "VerifyStatus": "string"
   },
   "StartTime": number,
   "Status": "string",
   "TaskExecutionArn": "string"
}
```

## Response Elements<a name="API_DescribeTaskExecution_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [BytesTransferred](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-BytesTransferred"></a>
The physical number of bytes transferred over the network\.  
Type: Long

 ** [BytesWritten](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-BytesWritten"></a>
The number of logical bytes written to the destination AWS storage resource\.  
Type: Long

 ** [EstimatedBytesToTransfer](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-EstimatedBytesToTransfer"></a>
The estimated physical number of bytes that is to be transferred over the network\.  
Type: Long

 ** [EstimatedFilesToTransfer](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-EstimatedFilesToTransfer"></a>
The expected number of files that is to be transferred over the network\. This value is calculated during the PREPARING phase, before the TRANSFERRING phase\. This value is the expected number of files to be transferred\. It's calculated based on comparing the content of the source and destination locations and finding the delta that needs to be transferred\.   
Type: Long

 ** [Excludes](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-Excludes"></a>
A list of filter rules that determines which files to exclude from a task\. The list should contain a single filter string that consists of the patterns to exclude\. The patterns are delimited by "\|" \(that is, a pipe\), for example: `"/folder1|/folder2"`   
   
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.

 ** [FilesTransferred](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-FilesTransferred"></a>
The actual number of files that was transferred over the network\. This value is calculated and updated on an ongoing basis during the TRANSFERRING phase\. It's updated periodically when each file is read from the source and sent over the network\.   
If failures occur during a transfer, this value can be less than `EstimatedFilesToTransfer`\. This value can also be greater than `EstimatedFilesTransferred` in some cases\. This element is implementation\-specific for some location types, so don't use it as an indicator for a correct file number or to monitor your task execution\.  
Type: Long

 ** [Includes](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-Includes"></a>
A list of filter rules that determines which files to include when running a task\. The list should contain a single filter string that consists of the patterns to include\. The patterns are delimited by "\|" \(that is, a pipe\), for example: `"/folder1|/folder2"`   
   
Type: Array of [FilterRule](API_FilterRule.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 1 item\.

 ** [Options](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-Options"></a>
Represents the options that are available to control the behavior of a [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html) operation\. Behavior includes preserving metadata such as user ID \(UID\), group ID \(GID\), and file permissions, and also overwriting files in the destination, data integrity verification, and so on\.  
A task has a set of default options associated with it\. If you don't specify an option in [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html), the default value is used\. You can override the defaults options on each task execution by specifying an overriding `Options` value to [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html)\.  
Type: [Options](API_Options.md) object

 ** [Result](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-Result"></a>
The result of the task execution\.  
Type: [TaskExecutionResultDetail](API_TaskExecutionResultDetail.md) object

 ** [StartTime](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-StartTime"></a>
The time that the task execution was started\.  
Type: Timestamp

 ** [Status](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-Status"></a>
The status of the task execution\.   
For detailed information about task execution statuses, see [Understanding Task Statuses](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-tasks.html#understand-task-creation-statuses)\.  
Type: String  
Valid Values:` QUEUED | LAUNCHING | PREPARING | TRANSFERRING | VERIFYING | SUCCESS | ERROR` 

 ** [TaskExecutionArn](#API_DescribeTaskExecution_ResponseSyntax) **   <a name="DataSync-DescribeTaskExecution-response-TaskExecutionArn"></a>
The Amazon Resource Name \(ARN\) of the task execution that was described\. `TaskExecutionArn` is hierarchical and includes `TaskArn` for the task that was executed\.   
For example, a `TaskExecution` value with the ARN `arn:aws:datasync:us-east-1:111222333444:task/task-0208075f79cedf4a2/execution/exec-08ef1e88ec491019b` executed the task with the ARN `arn:aws:datasync:us-east-1:111222333444:task/task-0208075f79cedf4a2`\.   
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}/execution/exec-[0-9a-f]{17}$` 

## Errors<a name="API_DescribeTaskExecution_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeTaskExecution_Examples"></a>

### Example<a name="API_DescribeTaskExecution_Example_1"></a>

The following example returns information about the `TaskExecution` value specified in the sample request\.

#### Sample Request<a name="API_DescribeTaskExecution_Example_1_Request"></a>

```
{
  "TaskExecutionArn": "arn:aws:datasync:us-east-1:111222333444:task/task-08de6e6697796f026/execution/exec-04ce9d516d69bd52f"
}
```

### Example<a name="API_DescribeTaskExecution_Example_2"></a>

This example illustrates one usage of DescribeTaskExecution\.

#### Sample Response<a name="API_DescribeTaskExecution_Example_2_Response"></a>

```
{
   "BytesTransferred": "5000",
   "BytesWritten": "5000",
   "EstimatedBytesToTransfer": "5000",
   "EstimatedFilesToTransfer": "100",
   "FilesTransferred": "100",
   "Result": { 
      "ErrorCode": "??????",
      "ErrorDetail": "??????",
      "PrepareDuration": "100",
      "PrepareStatus": "SUCCESS",
      "TransferDuration": "60",
      "TransferStatus": "AVAILABLE",
      "VerifyDuration": "30",
      "VerifyStatus": "SUCCESS"
   },
   "StartTime": "1532660733.39",
   "Status": "SUCCESS",
   "OverrideOptions": { 
      "Atime": "BEST_EFFORT",
      "BytesPerSecond": "1000",
      "Gid": "NONE",
      "Mtime": "PRESERVE",
      "PosixPermissions": "PRESERVE",
      "PreserveDevices": "NONE",
      "PreserveDeletedFiles": "PRESERVE",
      "Uid": "NONE",
      "VerifyMode": "POINT_IN_TIME_CONSISTENT"
   },
   "TaskExecutionArn": "arn:aws:datasync:us-east-2:111222333444:task/task-08de6e6697796f026/execution/exec-04ce9d516d69bd52f"
}
```

## See Also<a name="API_DescribeTaskExecution_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeTaskExecution) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeTaskExecution) 