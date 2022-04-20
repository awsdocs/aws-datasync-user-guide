# TaskExecutionResultDetail<a name="API_TaskExecutionResultDetail"></a>

Describes the detailed result of a `TaskExecution` operation\. This result includes the time in milliseconds spent in each phase, the status of the task execution, and the errors encountered\.

## Contents<a name="API_TaskExecutionResultDetail_Contents"></a>

 ** ErrorCode **   <a name="DataSync-Type-TaskExecutionResultDetail-ErrorCode"></a>
Errors that AWS DataSync encountered during execution of the task\. You can use this error code to help troubleshoot issues\.  
Type: String  
Required: No

 ** ErrorDetail **   <a name="DataSync-Type-TaskExecutionResultDetail-ErrorDetail"></a>
Detailed description of an error that was encountered during the task execution\. You can use this information to help troubleshoot issues\.   
Type: String  
Required: No

 ** PrepareDuration **   <a name="DataSync-Type-TaskExecutionResultDetail-PrepareDuration"></a>
The total time in milliseconds that AWS DataSync spent in the PREPARING phase\.   
Type: Long  
Valid Range: Minimum value of 0\.  
Required: No

 ** PrepareStatus **   <a name="DataSync-Type-TaskExecutionResultDetail-PrepareStatus"></a>
The status of the PREPARING phase\.  
Type: String  
Valid Values:` PENDING | SUCCESS | ERROR`   
Required: No

 ** TotalDuration **   <a name="DataSync-Type-TaskExecutionResultDetail-TotalDuration"></a>
The total time in milliseconds that AWS DataSync took to transfer the file from the source to the destination location\.  
Type: Long  
Valid Range: Minimum value of 0\.  
Required: No

 ** TransferDuration **   <a name="DataSync-Type-TaskExecutionResultDetail-TransferDuration"></a>
The total time in milliseconds that AWS DataSync spent in the TRANSFERRING phase\.  
Type: Long  
Valid Range: Minimum value of 0\.  
Required: No

 ** TransferStatus **   <a name="DataSync-Type-TaskExecutionResultDetail-TransferStatus"></a>
The status of the TRANSFERRING phase\.  
Type: String  
Valid Values:` PENDING | SUCCESS | ERROR`   
Required: No

 ** VerifyDuration **   <a name="DataSync-Type-TaskExecutionResultDetail-VerifyDuration"></a>
The total time in milliseconds that AWS DataSync spent in the VERIFYING phase\.  
Type: Long  
Valid Range: Minimum value of 0\.  
Required: No

 ** VerifyStatus **   <a name="DataSync-Type-TaskExecutionResultDetail-VerifyStatus"></a>
The status of the VERIFYING phase\.  
Type: String  
Valid Values:` PENDING | SUCCESS | ERROR`   
Required: No

## See Also<a name="API_TaskExecutionResultDetail_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/TaskExecutionResultDetail) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/TaskExecutionResultDetail) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/TaskExecutionResultDetail) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/TaskExecutionResultDetail) 