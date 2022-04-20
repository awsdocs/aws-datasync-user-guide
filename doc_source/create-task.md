# Configure task settings<a name="create-task"></a>

After you have created an AWS DataSync agent and configured the source and destination locations, you can configure the settings for a new task\. A task is a set of two locations \(source and destination\) and a set of options that you use to control the behavior of the task\.

You configure task settings when creating a new task in the AWS DataSync console\. You can also edit task settings by opening the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/), selecting the task you want to edit, and choosing **Edit**\. 

On the **Configure settings** page, for **Task name \- *optional***, enter a name for your task\. **Task name** is an optional setting\. 

The **Options** section contains configuration options for running your task\. The following sections provide more details about these options\.

**Topics**
+ [Data verification options](#configure-data-verification-options)
+ [Ownership and permissions\-related options](#configure-ownership-and-permissions)
+ [File metadata options and file management](#configure-file)
+ [Bandwidth options](#configure-bandwidth)
+ [Filtering options](#configure-filter)
+ [Scheduling and queueing options](#configure-scheduling-queueing)
+ [Tags and logging options](#configure-logging)

## Data verification options<a name="configure-data-verification-options"></a>

As DataSync transfers data, it always performs data integrity checks during the transfer\. You can enable additional verification to compare source and destination at the end of a transfer\. This additional check can verify the entire dataset or only the files that were transferred as part of the task execution\. For most use cases, we recommend verifying only the files transferred\.

Task data verification options specify how to verify data that's transferred by the task\.

Data verification options are as follows:
+  **Verify only the data transferred \(recommended\)** – This option calculates the checksum of transferred files and metadata on the source\. It then compares this checksum to the checksum calculated on those files at the destination at the end of the transfer\. We recommend this option when transferring to S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage classes\. For more information, see [Considerations when working with Amazon S3 storage classes in DataSync](create-s3-location.md#using-storage-classes)\.
+  **Verify all data in the destination** – This option performs a scan at the end of the transfer of the entire source and entire destination to verify that source and destination are fully synchronized\. You can't use this option when transferring to S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage classes\. For more information, see [Considerations when working with Amazon S3 storage classes in DataSync](create-s3-location.md#using-storage-classes)\. 
+  **Check integrity during the transfer** – This option doesn't run additional verification at the end of the transfer\. All data transmissions are still integrity\-checked with checksum verification during the transfer\.

## Ownership and permissions\-related options<a name="configure-ownership-and-permissions"></a>

DataSync preserves metadata between storage systems that have similar metadata structures\. Different options are used to configure such metadata preservation depending on the storage system type\.

 **When copying data between Network File System \(NFS\), Hadoop Distributed File System \(HDFS\), Amazon EFS, Amazon FSx for Lustre, Amazon FSx for OpenZFS, and Amazon S3, choose one of the following \(if applicable\):** 
+ Choose **Copy ownership** to have DataSync copy POSIX file and folder ownership, such as the group ID of the file's owners and the user ID of the file's owner\.
+ Choose **Copy permissions** to have DataSync copy POSIX permissions for files and folders from the source to the destination\.

 **When copying between Server Message Block \(SMB\) and FSx for Windows File Server, or between two FSx for Windows File Server locations, choose one of the following \(if applicable\):**
+ Choose **Copy ownership, DACLs, and SACLs** to have DataSync copy the following:
  + The object owner\.
  + NTFS discretionary access lists \(DACLs\), which determine whether to grant access to an object\.
  + NTFS system access control lists \(SACLs\), which are used by administrators to log attempts to access a secured object\.

  Copying SACLs requires granting additional permissions to the Windows user that DataSync uses to access your SMB location\. See [user](create-smb-location.md#SMBuser) to learn more about choosing a user name that ensures sufficient permissions to files, folders, and metadata\. 
+ Choose **Copy ownership and DACLs** to have DataSync copy the following:
  + The object owner\.
  + NTFS discretionary access lists \(DACLs\), which determine whether to grant access to an object\.

  DataSync won't copy NTFS system access control lists \(SACLs\) when you choose this option\.
+ Choose **Do not copy ownership or ACLs** if you want DataSync not to copy any ownership or permissions data\. The objects that DataSync writes to your destination location are owned by the user whose credentials are provided for DataSync to access the destination location\. Destination object permissions are determined based on the permissions configured on the destination server\.

For more information about metadata preservation using DataSync, see [How DataSync handles metadata and special files](special-files.md)\. 

## File metadata options and file management<a name="configure-file"></a>

You can configure DataSync tasks to copy file metadata, to keep deleted files, and to overwrite files in the destination\. These option settings are as follows: 
+ Choose **Copy timestamps** to have DataSync copy the timestamp metadata from the source to the destination\.
+ Choose **Keep deleted files** to have DataSync keep files in the destination that don't exist in the source file system\.

  If your task deletes objects, from your Amazon S3 bucket, you might incur minimum storage duration charges for certain storage classes\. For detailed information, see [Considerations when working with Amazon S3 storage classes in DataSync](create-s3-location.md#using-storage-classes)\.
+ Choose **Overwrite files** if you want files at the destination to be overwritten by files from the source when the source data or metadata is different\. 

  If you don't choose this option, the destination file isn't replaced by the source file, even if the destination file differs from the source file\.

  If your task overwrites objects, you might incur additional charges for certain storage classes \(for example, for retrieval or early deletion\)\. For detailed information, see [Considerations when working with Amazon S3 storage classes in DataSync](create-s3-location.md#using-storage-classes)\.

## Bandwidth options<a name="configure-bandwidth"></a>

 You can configure a bandwidth limit for DataSync tasks\. Bandwidth limit options are as follows: 
+ Choose **Use available** to have DataSync use all the network bandwidth that is available for the transfer\.
+ Choose **Set bandwidth limit \(MiB/s\)** to limit the maximum bandwidth that you want DataSync to use for this task\. 

  You can change bandwidth limits for an in\-progress task execution\. For more information, see [Adjusting bandwidth throttling for a task execution](working-with-task-executions.md#adjust-bandwidth-throttling)\.

## Filtering options<a name="configure-filter"></a>

When you transfer data from your source to your destination location, you can apply filters to transfer only a subset of the files in your source location\. The configuration options for filtering are as follows\. 
+ In the **Data transfer configuration** section, use the **Exclude patterns** section to specify files, folders, and objects to exclude from your transfer\. To include specific files, folders, and objects in your transfer, select **Specific files and folders** and then use the **Include patterns** section\. 
+ To add additional patterns to your filters, choose **Add pattern**\. For detailed information about filtering and syntax for creating patterns, see [Filtering the data transferred by DataSync](filtering.md)\. 
+ You can modify filter patterns when you edit a task\. You can also specify different patterns each time that you execute a task\.

## Scheduling and queueing options<a name="configure-scheduling-queueing"></a>

You can schedule a DataSync task to be run at a specific time\. If you are using a single agent to run multiple tasks, you can queue those tasks\. Configuring options for scheduling are as follows: 
+ In the **Schedule \(optional\)** section, configure your task to run on a schedule that you specify, with a minimum interval of 1 hour\.
+ For **Frequency**, configure how frequently you want the task to run\. For frequency configuration options, see [Configuring a task schedule](task-scheduling.md#configure-task-schedule)\.

If you are using a single agent to run multiple tasks, choose **Queueing** to make the tasks run in series \(first in, first out\)\. For more information, see [Queueing task executions](run-task.md#queue-task-execution)\.

## Tags and logging options<a name="configure-logging"></a>

 You can add one or more tags to a DataSync task\. A tag is a key\-value pair that is associated with the task\. You can also choose logging options to have DataSync publish logs for individual files or objects to the CloudWatch log group that you specify\. Tags and logging options are as follows: 
+ In the **Tags \- *optional*** section, enter **Key** and **Value** to tag your task\. A *tag* is a key\-value pair that helps you manage, filter, and search for your tasks\. We recommend that you create a name tag for your task\. 
+ Choose **Task logging \- *optional*** to have DataSync publish logs for individual files or objects to the CloudWatch log group that you specify\.

  To upload logs to your CloudWatch log group, DataSync requires a resource policy that grants sufficient permissions\. If you don't have a policy in the current Region, a check box appears so that you can create the required policy automatically\. For an example of such a policy, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\.

  For more information about using log groups and streams, see [ Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch Logs User Guide*\.

  Use the **Log level** option to set the level of detail that is logged to CloudWatch Logs\. Log level options include the following:
  + Choose **Log basic information such as transfer errors** to publish only basic information \(such as transfer errors\) to CloudWatch\.
  + Choose **Log all transferred objects, files, and folders ** to publish log records to CloudWatch Logs for all files or objects that the task copies and integrity checks\.
  + Choose **Do not send logs to CloudWatch** if you don't want DataSync logs to be published to CloudWatch\.

Choose **Next** to open the **Review** page\. 