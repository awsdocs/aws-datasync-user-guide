# TaskSchedule<a name="API_TaskSchedule"></a>

Specifies the schedule you want your task to use for repeated executions\. For more information, see [Schedule Expressions for Rules](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html)\.

## Contents<a name="API_TaskSchedule_Contents"></a>

 ** ScheduleExpression **   <a name="DataSync-Type-TaskSchedule-ScheduleExpression"></a>
A cron expression that specifies when AWS DataSync initiates a scheduled transfer from a source to a destination location\.   
Type: String  
Length Constraints: Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\ \_\*\?\,\|\^\-\/\#\s\(\)\+]*$`   
Required: Yes

## See Also<a name="API_TaskSchedule_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/TaskSchedule) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/TaskSchedule) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/TaskSchedule) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/TaskSchedule) 