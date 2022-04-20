# TaskFilter<a name="API_TaskFilter"></a>

You can use API filters to narrow down the list of resources returned by `ListTasks`\. For example, to retrieve all tasks on a source location, you can use `ListTasks` with filter name `LocationId` and `Operator Equals` with the ARN for the location\.

## Contents<a name="API_TaskFilter_Contents"></a>

 ** Name **   <a name="DataSync-Type-TaskFilter-Name"></a>
The name of the filter being used\. Each API call supports a list of filters that are available for it\. For example, `LocationId` for `ListTasks`\.  
Type: String  
Valid Values:` LocationId | CreationTime`   
Required: Yes

 ** Operator **   <a name="DataSync-Type-TaskFilter-Operator"></a>
The operator that is used to compare filter values \(for example, `Equals` or `Contains`\)\. For more about API filtering operators, see [API filters for ListTasks and ListLocations](https://docs.aws.amazon.com/datasync/latest/userguide/query-resources.html)\.  
Type: String  
Valid Values:` Equals | NotEquals | In | LessThanOrEqual | LessThan | GreaterThanOrEqual | GreaterThan | Contains | NotContains | BeginsWith`   
Required: Yes

 ** Values **   <a name="DataSync-Type-TaskFilter-Values"></a>
The values that you want to filter for\. For example, you might want to display only tasks for a specific destination location\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^[0-9a-zA-Z_\ \-\:\*\.\\/\?-]*$`   
Required: Yes

## See Also<a name="API_TaskFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/TaskFilter) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/TaskFilter) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/TaskFilter) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/TaskFilter) 