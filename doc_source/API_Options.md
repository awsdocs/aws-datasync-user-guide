# Options<a name="API_Options"></a>

Represents the options that are available to control the behavior of a [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html) operation\. Behavior includes preserving metadata such as user ID \(UID\), group ID \(GID\), and file permissions, and also overwriting files in the destination, data integrity verification, and so on\.

A task has a set of default options associated with it\. If you don't specify an option in [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html), the default value is used\. You can override the defaults options on each task execution by specifying an overriding `Options` value to [StartTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_StartTaskExecution.html)\.

## Contents<a name="API_Options_Contents"></a>

 ** Atime **   <a name="DataSync-Type-Options-Atime"></a>
A file metadata value that shows the last time a file was accessed \(that is, when the file was read or written to\)\. If you set `Atime` to `BEST_EFFORT`, DataSync attempts to preserve the original `Atime` attribute on all source files \(that is, the version before the `PREPARING` phase\)\. However, `Atime`'s behavior is not fully standard across platforms, so AWS DataSync can only do this on a best\-effort basis\.   
Default value: `BEST_EFFORT`   
 `BEST_EFFORT`: Attempt to preserve the per\-file `Atime` value \(recommended\)\.  
 `NONE`: Ignore `Atime`\.  
If `Atime` is set to `BEST_EFFORT`, `Mtime` must be set to `PRESERVE`\.   
If `Atime` is set to `NONE`, `Mtime` must also be `NONE`\. 
Type: String  
Valid Values:` NONE | BEST_EFFORT`   
Required: No

 ** BytesPerSecond **   <a name="DataSync-Type-Options-BytesPerSecond"></a>
A value that limits the bandwidth used by AWS DataSync\. For example, if you want AWS DataSync to use a maximum of 1 MB, set this value to `1048576` \(`=1024*1024`\)\.  
Type: Long  
Valid Range: Minimum value of \-1\.  
Required: No

 ** Gid **   <a name="DataSync-Type-Options-Gid"></a>
The POSIX group ID \(GID\) of the file's owners\.  
For more information, see [Metadata copied by DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html#metadata-copied)\.  
Default value: `INT_VALUE`\. This preserves the integer value of the ID\.  
 `INT_VALUE`: Preserve the integer value of user ID \(UID\) and GID \(recommended\)\.  
 `NONE`: Ignore UID and GID\.  
Type: String  
Valid Values:` NONE | INT_VALUE | NAME | BOTH`   
Required: No

 ** LogLevel **   <a name="DataSync-Type-Options-LogLevel"></a>
A value that determines the type of logs that DataSync publishes to a log stream in the Amazon CloudWatch log group that you provide\. For more information about providing a log group for DataSync, see [CloudWatchLogGroupArn](https://docs.aws.amazon.com/datasync/latest/userguide/API_CreateTask.html#DataSync-CreateTask-request-CloudWatchLogGroupArn)\. If set to `OFF`, no logs are published\. `BASIC` publishes logs on errors for individual files transferred, and `TRANSFER` publishes logs for every file or object that is transferred and integrity checked\.  
Type: String  
Valid Values:` OFF | BASIC | TRANSFER`   
Required: No

 ** Mtime **   <a name="DataSync-Type-Options-Mtime"></a>
A value that indicates the last time that a file was modified \(that is, a file was written to\) before the `PREPARING` phase\. This option is required for cases when you need to run the same task more than one time\.   
Default Value: `PRESERVE`   
 `PRESERVE`: Preserve original `Mtime` \(recommended\)  
 `NONE`: Ignore `Mtime`\.   
If `Mtime` is set to `PRESERVE`, `Atime` must be set to `BEST_EFFORT`\.  
If `Mtime` is set to `NONE`, `Atime` must also be set to `NONE`\. 
Type: String  
Valid Values:` NONE | PRESERVE`   
Required: No

 ** ObjectTags **   <a name="DataSync-Type-Options-ObjectTags"></a>
Specifies whether object tags are maintained when transferring between object storage systems\. If you want your DataSync task to ignore object tags, specify the `NONE` value\.  
Default Value: `PRESERVE`   
Type: String  
Valid Values:` PRESERVE | NONE`   
Required: No

 ** OverwriteMode **   <a name="DataSync-Type-Options-OverwriteMode"></a>
A value that determines whether files at the destination should be overwritten or preserved when copying files\. If set to `NEVER` a destination file will not be replaced by a source file, even if the destination file differs from the source file\. If you modify files in the destination and you sync the files, you can use this value to protect against overwriting those changes\.   
Some storage classes have specific behaviors that can affect your S3 storage cost\. For detailed information, see [Considerations when working with Amazon S3 storage classes in DataSync ](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes) in the * AWS DataSync User Guide*\.  
Type: String  
Valid Values:` ALWAYS | NEVER`   
Required: No

 ** PosixPermissions **   <a name="DataSync-Type-Options-PosixPermissions"></a>
A value that determines which users or groups can access a file for a specific purpose such as reading, writing, or execution of the file\.  
For more information, see [Metadata copied by DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html#metadata-copied)\.  
Default value: `PRESERVE`   
 `PRESERVE`: Preserve POSIX\-style permissions \(recommended\)\.  
 `NONE`: Ignore permissions\.   
 AWS DataSync can preserve extant permissions of a source location\.
Type: String  
Valid Values:` NONE | PRESERVE`   
Required: No

 ** PreserveDeletedFiles **   <a name="DataSync-Type-Options-PreserveDeletedFiles"></a>
A value that specifies whether files in the destination that don't exist in the source file system should be preserved\. This option can affect your storage cost\. If your task deletes objects, you might incur minimum storage duration charges for certain storage classes\. For detailed information, see [Considerations when working with Amazon S3 storage classes in DataSync ](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes) in the * AWS DataSync User Guide*\.  
Default value: `PRESERVE`   
 `PRESERVE`: Ignore such destination files \(recommended\)\.   
 `REMOVE`: Delete destination files that aren’t present in the source\.  
Type: String  
Valid Values:` PRESERVE | REMOVE`   
Required: No

 ** PreserveDevices **   <a name="DataSync-Type-Options-PreserveDevices"></a>
A value that determines whether AWS DataSync should preserve the metadata of block and character devices in the source file system, and re\-create the files with that device name and metadata on the destination\. DataSync does not copy the contents of such devices, only the name and metadata\.   
 AWS DataSync can't sync the actual contents of such devices, because they are nonterminal and don't return an end\-of\-file \(EOF\) marker\.
Default value: `NONE`   
 `NONE`: Ignore special devices \(recommended\)\.   
 `PRESERVE`: Preserve character and block device metadata\. This option isn't currently supported for Amazon EFS\.   
Type: String  
Valid Values:` NONE | PRESERVE`   
Required: No

 ** SecurityDescriptorCopyFlags **   <a name="DataSync-Type-Options-SecurityDescriptorCopyFlags"></a>
A value that determines which components of the SMB security descriptor are copied from source to destination objects\.   
This value is only used for transfers between SMB and Amazon FSx for Windows File Server locations, or between two Amazon FSx for Windows File Server locations\. For more information about how DataSync handles metadata, see [How DataSync Handles Metadata and Special Files](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html)\.   
Default value: `OWNER_DACL`   
 `OWNER_DACL`: For each copied object, DataSync copies the following metadata:  
+ Object owner\.
+ NTFS discretionary access control lists \(DACLs\), which determine whether to grant access to an object\.
When choosing this option, DataSync does NOT copy the NTFS system access control lists \(SACLs\), which are used by administrators to log attempts to access a secured object\.  
 `OWNER_DACL_SACL`: For each copied object, DataSync copies the following metadata:  
+ Object owner\.
+ NTFS discretionary access control lists \(DACLs\), which determine whether to grant access to an object\.
+ NTFS system access control lists \(SACLs\), which are used by administrators to log attempts to access a secured object\.
Copying SACLs requires granting additional permissions to the Windows user that DataSync uses to access your SMB location\. For information about choosing a user that ensures sufficient permissions to files, folders, and metadata, see [user](create-smb-location.html#SMBuser)\.  
 `NONE`: None of the SMB security descriptor components are copied\. Destination objects are owned by the user that was provided for accessing the destination location\. DACLs and SACLs are set based on the destination server’s configuration\.   
Type: String  
Valid Values:` NONE | OWNER_DACL | OWNER_DACL_SACL`   
Required: No

 ** TaskQueueing **   <a name="DataSync-Type-Options-TaskQueueing"></a>
A value that determines whether tasks should be queued before executing the tasks\. If set to `ENABLED`, the tasks will be queued\. The default is `ENABLED`\.  
If you use the same agent to run multiple tasks, you can enable the tasks to run in series\. For more information, see [Queueing task executions](https://docs.aws.amazon.com/datasync/latest/userguide/run-task.html#queue-task-execution)\.  
Type: String  
Valid Values:` ENABLED | DISABLED`   
Required: No

 ** TransferMode **   <a name="DataSync-Type-Options-TransferMode"></a>
A value that determines whether DataSync transfers only the data and metadata that differ between the source and the destination location, or whether DataSync transfers all the content from the source, without comparing to the destination location\.   
 `CHANGED`: DataSync copies only data or metadata that is new or different content from the source location to the destination location\.  
 `ALL`: DataSync copies all source location content to the destination, without comparing to existing content on the destination\.  
Type: String  
Valid Values:` CHANGED | ALL`   
Required: No

 ** Uid **   <a name="DataSync-Type-Options-Uid"></a>
The POSIX user ID \(UID\) of the file's owner\.  
For more information, see [Metadata copied by DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html#metadata-copied)\.  
Default value: `INT_VALUE`\. This preserves the integer value of the ID\.  
 `INT_VALUE`: Preserve the integer value of UID and group ID \(GID\) \(recommended\)\.  
 `NONE`: Ignore UID and GID\.   
Type: String  
Valid Values:` NONE | INT_VALUE | NAME | BOTH`   
Required: No

 ** VerifyMode **   <a name="DataSync-Type-Options-VerifyMode"></a>
A value that determines whether a data integrity verification should be performed at the end of a task execution after all data and metadata have been transferred\. For more information, see [Configure task settings](https://docs.aws.amazon.com/datasync/latest/userguide/create-task.html)\.   
Default value: `POINT_IN_TIME_CONSISTENT`   
 `ONLY_FILES_TRANSFERRED` \(recommended\): Perform verification only on files that were transferred\.   
 `POINT_IN_TIME_CONSISTENT`: Scan the entire source and entire destination at the end of the transfer to verify that source and destination are fully synchronized\. This option isn't supported when transferring to S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage classes\.  
 `NONE`: No additional verification is done at the end of the transfer, but all data transmissions are integrity\-checked with checksum verification during the transfer\.  
Type: String  
Valid Values:` POINT_IN_TIME_CONSISTENT | ONLY_FILES_TRANSFERRED | NONE`   
Required: No

## See Also<a name="API_Options_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/Options) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/Options) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/Options) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/Options) 