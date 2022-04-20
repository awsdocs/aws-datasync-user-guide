# ListLocations<a name="API_ListLocations"></a>

Returns a list of source and destination locations\.

If you have more locations than are returned in a response \(that is, the response returns only a truncated list of your agents\), the response contains a token that you can specify in your next request to fetch the next page of locations\.

## Request Syntax<a name="API_ListLocations_RequestSyntax"></a>

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

## Request Parameters<a name="API_ListLocations_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Filters](#API_ListLocations_RequestSyntax) **   <a name="DataSync-ListLocations-request-Filters"></a>
You can use API filters to narrow down the list of resources returned by `ListLocations`\. For example, to retrieve all tasks on a specific source location, you can use `ListLocations` with filter name `LocationType S3` and `Operator Equals`\.  
Type: Array of [LocationFilter](API_LocationFilter.md) objects  
Required: No

 ** [MaxResults](#API_ListLocations_RequestSyntax) **   <a name="DataSync-ListLocations-request-MaxResults"></a>
The maximum number of locations to return\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListLocations_RequestSyntax) **   <a name="DataSync-ListLocations-request-NextToken"></a>
An opaque string that indicates the position at which to begin the next list of locations\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`   
Required: No

## Response Syntax<a name="API_ListLocations_ResponseSyntax"></a>

```
{
   "Locations": [ 
      { 
         "LocationArn": "string",
         "LocationUri": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListLocations_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Locations](#API_ListLocations_ResponseSyntax) **   <a name="DataSync-ListLocations-response-Locations"></a>
An array that contains a list of locations\.  
Type: Array of [LocationListEntry](API_LocationListEntry.md) objects

 ** [NextToken](#API_ListLocations_ResponseSyntax) **   <a name="DataSync-ListLocations-response-NextToken"></a>
An opaque string that indicates the position at which to begin returning the next list of locations\.  
Type: String  
Length Constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+` 

## Errors<a name="API_ListLocations_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_ListLocations_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/ListLocations) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/ListLocations) 