# CancelTaskExecution<a name="API_CancelTaskExecution"></a>

Stops an AWS DataSync task execution that's in progress\. The transfer of some files are abruptly interrupted\. File contents that're transferred to the destination might be incomplete or inconsistent with the source files\.

However, if you start a new task execution using the same task and allow it to finish, file content on the destination will be complete and consistent\. This applies to other unexpected failures that interrupt a task execution\. In all of these cases, DataSync successfully completes the transfer when you start the next task execution\.

## Request Syntax<a name="API_CancelTaskExecution_RequestSyntax"></a>

```
{
   "TaskExecutionArn": "string"
}
```

## Request Parameters<a name="API_CancelTaskExecution_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [TaskExecutionArn](#API_CancelTaskExecution_RequestSyntax) **   <a name="DataSync-CancelTaskExecution-request-TaskExecutionArn"></a>
The Amazon Resource Name \(ARN\) of the task execution to cancel\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]*:[0-9]{12}:task/task-[0-9a-f]{17}/execution/exec-[0-9a-f]{17}$`   
Required: Yes

## Response Elements<a name="API_CancelTaskExecution_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_CancelTaskExecution_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CancelTaskExecution_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CancelTaskExecution) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CancelTaskExecution) 