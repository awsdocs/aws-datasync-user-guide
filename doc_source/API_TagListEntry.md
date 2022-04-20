# TagListEntry<a name="API_TagListEntry"></a>

Represents a single entry in a list of AWS resource tags\. `TagListEntry` returns an array that contains a list of tasks when the [ListTagsForResource](https://docs.aws.amazon.com/datasync/latest/userguide/API_ListTagsForResource.html) operation is called\.

## Contents<a name="API_TagListEntry_Contents"></a>

 ** Key **   <a name="DataSync-Type-TagListEntry-Key"></a>
The key for an AWS resource tag\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:/-]+$`   
Required: Yes

 ** Value **   <a name="DataSync-Type-TagListEntry-Value"></a>
The value for an AWS resource tag\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`   
Required: No

## See Also<a name="API_TagListEntry_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/TagListEntry) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/TagListEntry) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/TagListEntry) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/TagListEntry) 