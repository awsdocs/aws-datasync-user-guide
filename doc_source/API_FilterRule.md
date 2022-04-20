# FilterRule<a name="API_FilterRule"></a>

Specifies which files, folders, and objects to include or exclude when transferring files from source to destination\.

## Contents<a name="API_FilterRule_Contents"></a>

 ** FilterType **   <a name="DataSync-Type-FilterRule-FilterType"></a>
The type of filter rule to apply\. AWS DataSync only supports the SIMPLE\_PATTERN rule type\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^[A-Z0-9_]+$`   
Valid Values:` SIMPLE_PATTERN`   
Required: No

 ** Value **   <a name="DataSync-Type-FilterRule-Value"></a>
A single filter string that consists of the patterns to include or exclude\. The patterns are delimited by "\|" \(that is, a pipe\), for example: `/folder1|/folder2`   
   
Type: String  
Length Constraints: Maximum length of 102400\.  
Pattern: `^[^\x00]+$`   
Required: No

## See Also<a name="API_FilterRule_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/FilterRule) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/FilterRule) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/FilterRule) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/FilterRule) 