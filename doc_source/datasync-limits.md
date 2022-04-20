# AWS DataSync quotas and limits<a name="datasync-limits"></a>

Following, you can find information on AWS DataSync resources and their quotas and limits\.

**Topics**
+ [Quotas for tasks](#task-hard-limits)
+ [Quotas for task executions](#task-execution-retention)
+ [Limits for DataSync file systems](#file-system-limits)
+ [Limits for DataSync filters](#filter-limits)

## Quotas for tasks<a name="task-hard-limits"></a>

Following are the quotas on tasks for each customer account in an AWS Region\.


| Resource | Quota | Can quota be increased? | 
| --- | --- | --- | 
|  Maximum number of tasks you can create in account per AWS Region  |  100  |  Yes  | 
|  Maximum number of files per task, when transferring data between self\-managed storage and AWS services  |  50 million  For tasks that transfer more than 20 million files, make sure that you allocate a minimum of 64 GB of RAM to the virtual machine \(VM\)\. For minimum resource requirements for DataSync, see [Virtual machine requirements](agent-requirements.md#hardware)\.   |  Yes  As an alternative to requesting an increase, you can create tasks on different subdirectories using include/exclude filters\. For more information about using filters, see [Filtering the data transferred by AWS DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html)\.    | 
|  Maximum number of files per task, when transferring data between AWS storage services  |  25 million  |  Yes  As an alternative to requesting an increase, you can create tasks on different subdirectories using include/exclude filters\. For more information about using filters, see [Filtering the data transferred by AWS DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html)\.    | 
|  Maximum number of files per task, when running DataSync on an AWS Snowcone device  |  200,000  |  No  | 
|  Maximum throughput per task  |  10 Gbps  |  No  | 

You can take the following steps to request an increase for the permitted quotas\. These increases are not granted right away, so it might take a couple of days for your increase to take effect\.

**To request a quota increase**

1. Open the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in if necessary, and then choose **Create case**\.

1. For **Create case**, choose **Service limit increase**\.

1. For **Limit type**, choose **DataSync**\.

1. For **Region**, select your AWS Region, and for **Limit**, select the quota that you want to increase\.

1. Fill in the case description, and then choose your preferred method of contact\.

   If you need to increase a different quota, fill out a separate request\. 

## Quotas for task executions<a name="task-execution-retention"></a>

Following are the quotas on task executions for each customer account in an AWS Region\.


| Resource | Quota | 
| --- | --- | 
|  Number of days task execution history is retained  |  30  | 

## Limits for DataSync file systems<a name="file-system-limits"></a>

The following table lists file system limits for DataSync\. 

If the storage systems at the source and destination locations have higher limits on the lengths of the total path and path components \(file names, directories, and subdirectories\), DataSync might not be able to access some objects on those systems\. 


| Description | Limit | 
| --- | --- | 
|  Maximum total file path length  |  4096 bytes  | 
|  Maximum file path component \(file name, directory, or subdirectory\) length  |  255 bytes  | 
|  Maximum length of Windows domain  |  253 characters  | 
|  Maximum length of server hostname  |  255 characters  | 
|  Maximum Amazon S3 object name length  |  1024 UTF\-8 characters  | 

## Limits for DataSync filters<a name="filter-limits"></a>

Following are the limits on DataSync filters per task or task execution\.


| Filter | Limit | 
| --- | --- | 
|  Maximum number of characters in a filter string  |  409,600  | 