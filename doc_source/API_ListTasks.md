# ListTasks<a name="API_ListTasks"></a>

Returns a list of the AWS DataSync tasks you created\.

## Request Syntax<a name="API_ListTasks_RequestSyntax"></a>

```
{
   "Filters": [ 
      { 
         "Name": "string",
         "Operator": "string",
         "Values": [ "string" ]
      }
   ],
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListTasks_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Filters](#API_ListTasks_RequestSyntax) **   <a name="DataSync-ListTasks-request-Filters"></a>
You can use API filters to narrow down the list of resources returned by `ListTasks`\. For example, to retrieve all tasks on a specific source location, you can use `ListTasks` with filter name `LocationId` and `Operator Equals` with the ARN for the location\.  
Type: Array of [TaskFilter](API_TaskFilter.md) objects  
Required: No

 ** [MaxResults](#API_ListTasks_RequestSyntax) **   <a name="DataSync-ListTasks-request-MaxResults"></a>
The maximum number of tasks to return\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListTasks_RequestSyntax) **   <a name="DataSync-ListTasks-request-NextToken"></a>
An opaque string that indicates the position at which to begin the next list of tasks\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`   
Required: No

## Response Syntax<a name="API_ListTasks_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "Tasks": [ 
      { 
         "Name": "string",
         "Status": "string",
         "TaskArn": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListTasks_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListTasks_ResponseSyntax) **   <a name="DataSync-ListTasks-response-NextToken"></a>
An opaque string that indicates the position at which to begin returning the next list of tasks\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+` 

 ** [Tasks](#API_ListTasks_ResponseSyntax) **   <a name="DataSync-ListTasks-response-Tasks"></a>
A list of all the tasks that are returned\.  
Type: Array of [TaskListEntry](API_TaskListEntry.md) objects

## Errors<a name="API_ListTasks_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_ListTasks_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/ListTasks) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/ListTasks) 