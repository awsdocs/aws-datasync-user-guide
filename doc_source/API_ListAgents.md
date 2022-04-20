# ListAgents<a name="API_ListAgents"></a>

Returns a list of agents owned by an AWS account in the AWS Region specified in the request\. The returned list is ordered by agent Amazon Resource Name \(ARN\)\.

By default, this operation returns a maximum of 100 agents\. This operation supports pagination that enables you to optionally reduce the number of agents returned in a response\.

If you have more agents than are returned in a response \(that is, the response returns only a truncated list of your agents\), the response contains a marker that you can specify in your next request to fetch the next page of agents\.

## Request Syntax<a name="API_ListAgents_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListAgents_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListAgents_RequestSyntax) **   <a name="DataSync-ListAgents-request-MaxResults"></a>
The maximum number of agents to list\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListAgents_RequestSyntax) **   <a name="DataSync-ListAgents-request-NextToken"></a>
An opaque string that indicates the position at which to begin the next list of agents\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`   
Required: No

## Response Syntax<a name="API_ListAgents_ResponseSyntax"></a>

```
{
   "Agents": [ 
      { 
         "AgentArn": "string",
         "Name": "string",
         "Status": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListAgents_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Agents](#API_ListAgents_ResponseSyntax) **   <a name="DataSync-ListAgents-response-Agents"></a>
A list of agents in your account\.  
Type: Array of [AgentListEntry](API_AgentListEntry.md) objects

 ** [NextToken](#API_ListAgents_ResponseSyntax) **   <a name="DataSync-ListAgents-response-NextToken"></a>
An opaque string that indicates the position at which to begin returning the next list of agents\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+` 

## Errors<a name="API_ListAgents_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_ListAgents_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/ListAgents) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/ListAgents) 