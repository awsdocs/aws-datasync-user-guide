# ListTagsForResource<a name="API_ListTagsForResource"></a>

Returns all the tags associated with a specified resource\. 

## Request Syntax<a name="API_ListTagsForResource_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "ResourceArn": "string"
}
```

## Request Parameters<a name="API_ListTagsForResource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListTagsForResource_RequestSyntax) **   <a name="DataSync-ListTagsForResource-request-MaxResults"></a>
The maximum number of locations to return\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListTagsForResource_RequestSyntax) **   <a name="DataSync-ListTagsForResource-request-NextToken"></a>
An opaque string that indicates the position at which to begin the next list of locations\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`   
Required: No

 ** [ResourceArn](#API_ListTagsForResource_RequestSyntax) **   <a name="DataSync-ListTagsForResource-request-ResourceArn"></a>
The Amazon Resource Name \(ARN\) of the resource whose tags to list\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:(agent|task|location)/(agent|task|loc)-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_ListTagsForResource_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListTagsForResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListTagsForResource_ResponseSyntax) **   <a name="DataSync-ListTagsForResource-response-NextToken"></a>
An opaque string that indicates the position at which to begin returning the next list of resource tags\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+` 

 ** [Tags](#API_ListTagsForResource_ResponseSyntax) **   <a name="DataSync-ListTagsForResource-response-Tags"></a>
Array of resource tags\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 55 items\.

## Errors<a name="API_ListTagsForResource_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_ListTagsForResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/ListTagsForResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/ListTagsForResource) 