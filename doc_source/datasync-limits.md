# AWS DataSync quotas<a name="datasync-limits"></a>

Find out about quotas when working with AWS DataSync\.

## Storage system quotas<a name="file-system-limits"></a>

DataSync has quotas when working with storage system files and objects\.


| Description | Limit | 
| --- | --- | 
|  Maximum total file path length  |  4,096 bytes  | 
|  Maximum file path component \(file name, directory, or subdirectory\) length  |  255 bytes  | 
|  Maximum length of Windows domain  |  253 characters  | 
|  Maximum length of server hostname  |  255 characters  | 
|  Maximum Amazon S3 object name length  |  1,024 UTF\-8 characters  | 

## Task quotas<a name="task-hard-limits"></a>

These are the quotas on DataSync tasks for each AWS account in an AWS Region\.


| Resource | Quota | Can quota be increased? | 
| --- | --- | --- | 
|  Maximum number of tasks you can create  |  100  |  Yes  | 
|  Maximum number of files or objects per task when transferring data between self\-managed storage and AWS services  |  50 million  For tasks that transfer more than 20 million files or objects, make sure that you allocate a minimum of 64 GB of RAM to the virtual machine \(VM\)\. For minimum resource requirements for DataSync, see [Virtual machine requirements](agent-requirements.md#hardware)\.   |  Yes  As an alternative to requesting an increase, you can create tasks on different subdirectories using include and exclude filters\. For more information about using filters, see [Filtering the data transferred by AWS DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html)\.    | 
|  Maximum number of files or objects per task when transferring data between AWS storage services  |  25 million  |  Yes  As an alternative to requesting an increase, you can create tasks on different subdirectories using include/exclude filters\. For more information about using filters, see [Filtering the data transferred by AWS DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html)\.    | 
|  Maximum number of files per task when running DataSync on an AWS Snowcone device  |  200,000  |  No  | 
|  Maximum throughput per task  |  10 Gbps  |  No  | 

## Task filter quotas<a name="filter-limits"></a>

DataSync has quotas on how you can filter data in a task\.


| Filter | Limit | 
| --- | --- | 
|  Maximum number of characters you can include in a task filter  |  102,400 characters  If you're using the AWS Management Console, this limit includes all the characters combined in your include and exclude patterns\.   | 

## Task execution quotas<a name="task-execution-retention"></a>

These are the quotas on DataSync task executions for each AWS account in an AWS Region\.


| Resource | Quota | 
| --- | --- | 
|  Number of days a task execution's history is retained  |  30  | 

## Request a quota increase<a name="request-quota-increase"></a>

You can request an increase for some DataSync quotas\. Increases aren't granted right away and might take a couple of days to take effect\.

**To request a quota increase**

1. Open the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in if necessary, and then choose **Create case**\.

1. For **Create case**, choose **Service limit increase**\.

1. For **Limit type**, choose **DataSync**\.

1. For **Region**, select your AWS Region, and for **Limit**, select the quota that you want to increase\.

1. Fill in the case description, and then choose your preferred method of contact\.

   If you need to increase a different quota, fill out a separate request\. 