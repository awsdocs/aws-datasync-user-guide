# How AWS DataSync works<a name="how-datasync-works"></a>

In this section, you can find information about components, terms, and how DataSync works\.

**Topics**
+ [AWS DataSync architecture](#datasync-archtecture)
+ [Components and terminology](#terminology)
+ [How DataSync transfers files](#transfering-files)

## AWS DataSync architecture<a name="datasync-archtecture"></a>

**Topics**
+ [Data transfer between self\-managed storage and AWS](#onprem-aws)
+ [Data transfer between AWS storage services](#in-cloud-transfer)
+ [Data transfer using an agent deployed in a Region](#ec2-agent-in-region)

The architectural diagrams show how DataSync transfers data between on\-premises \(self\-managed\) storage systems and AWS storage services, and between in\-cloud storage systems and AWS storage services\. 

For a list of all DataSync supported source and destination endpoints, see [Working with locations](working-with-locations.md)\.

### Data transfer between self\-managed storage and AWS<a name="onprem-aws"></a>

The following diagram shows a high\-level view of the DataSync architecture for transferring files between self\-managed storage and AWS services\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/DataSync-chart-on-prem.png)

### Data transfer between AWS storage services<a name="in-cloud-transfer"></a>

The following diagram provides a high\-level view of the DataSync architecture for transferring files between AWS services within the same AWS account\. This architecture applies to both in\-Region and cross\-Region transfers\.

With these kinds of transfers, traffic remains in the AWS network and doesn't traverse the public internet\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/DataSync-chart-agentless.png)

**Important**  
When you use DataSync to copy files or objects between AWS Regions, you pay for data transfer between Regions\. This is billed as data transfer OUT from your source Region to your destination Region\. For more information, see [Data transfer pricing](http://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)\. 

### Data transfer using an agent deployed in a Region<a name="ec2-agent-in-region"></a>

You can use DataSync to transfer data between AWS services in different AWS accounts, or between self\-managed file systems in AWS and Amazon S3\. To do so, you can deploy the DataSync agent as an Amazon EC2 instance in an AWS Region\. For more information, see [Deploying your DataSync agent in AWS Regions](using-ec2-agent-in-region.md)\.

## Components and terminology<a name="terminology"></a>

The components of DataSync include the following:
+ **Agent**: A virtual machine \(VM\) that's used to read data from or write data to a self\-managed location\. An agent isn't required when transferring between AWS storage services in the same AWS account\. 
+ **Location**: Any source or destination location included in the data transfer\. This can include Amazon S3, Amazon EFS, Amazon FSx for Windows File Server, Amazon FSx for Lustre, Amazon FSx for OpenZFS, Network File System \(NFS\), Server Message Block \(SMB\), Hadoop Distributed File System \(HDFS\), or self\-managed object storage\. 
+ **Task**: A source location and a destination location, and a configuration that defines how data is transferred\. A task always transfers data from the source to the destination\. The configuration can include options such as the task schedule, bandwidth limit, and so on\. A task is the complete definition of a data transfer\. 
+ **Task execution**: An individual run of a task, which includes information such as the start time, end time, bytes written, and status\. 

### Agent<a name="sync-agents"></a>

An *agent* is a VM that you own that's used to read or write data from self\-managed storage systems\. The agent can be deployed on VMware ESXi, Linux Kernel\-based Virtual Machine \(KVM\), Microsoft Hyper\-V hypervisors, or it can be launched as an Amazon EC2 instance\. You use the AWS DataSync console or the API to set up and activate your agent\. The activation process associates your agent VM with your AWS account\. For information about agents, see [Working with agents](working-with-agents.md)\. 

An agent that's functioning properly has the status **ONLINE**\. If an agent is unable to communicate with AWS, it transitions to **OFFLINE** status\. This transition can result from issues with a network partition, firewall misconfiguration, and other events that make the agent VM unable to connect to AWS\. The status of an agent that's powered off also shows as **OFFLINE**\.

### Location<a name="sync-locations"></a>

A *location* is where you're copying data from and to\. Each task has two locations—a source and destination location\. DataSync supports the following location types: 
+ Network File System \(NFS\)
+ Server Message Block \(SMB\)
+ Hadoop Distributed File System \(HDFS\)
+ On\-premises \(self\-managed\) object storage
+ Amazon EFS
+ Amazon FSx for Windows File Server
+ Amazon FSx for Lustre
+ Amazon FSx for OpenZFS
+ Amazon S3

For more information, see [Working with locations](working-with-locations.md)\.

### Task<a name="tasks"></a>

A *task* describes a DataSync transfer\. It identifies a source and destination location along with details about how to copy data between those locations\. You also can specify how a task treats metadata, deleted files, and permissions\.

### Task execution<a name="task-executions"></a>

A *task execution* is an individual run of a task, which shows information such as the start time, end time, number of transferred files, and status\. 

A task execution has five transition phases and two terminal statuses, as shown in the following diagram\. These phases and statuses are:
+ **QUEUEING** – This phase consists of queuing the task executions that are running using the same agent\.
+ **LAUNCHING** – During this phase, the task execution is initialized\.
+ **PREPARING** – During this phase, DataSync computes which files need to be transferred\.
+ **TRANSFERRING** – During this phase, DataSync transfers data to AWS\.
+ **VERIFYING** – During this optional phase, DataSync performs a full data and metadata integrity verification\. This phase occurs only if the `VerifyMode` option is enabled during configuration\.
+ **SUCCESS** or **ERROR** – When the task is finished, DataSync sets the task to one of these terminal statuses, depending on whether it was successful\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/aws-sync-v8.png)

If the `VerifyMode` option isn't enabled in the task configuration, the terminal status is set after the **TRANSFERRING** phase\. Otherwise, it is set after the **VERIFYING** phase\. The two terminal statuses are these:
+ **SUCCESS**
+ **ERROR**

For more information, see [Task execution statuses](working-with-task-executions.md#understand-task-execution-statuses)\.

## How DataSync transfers files<a name="transfering-files"></a>

**Topics**
+ [How AWS DataSync verifies data integrity](#how-verifying-works)
+ [How DataSync handles open and locked files](#open-locked-files)

When a task starts, it goes through different phases: **LAUNCHING**, **PREPARING**, **TRANSFERRING**, and **VERIFYING**\. In the **LAUNCHING** phase, DataSync initializes the task execution\. In the **PREPARING** phase, DataSync examines the source and destination file systems to determine which files to sync\. It does so by recursively scanning the contents and metadata of files on the source and destination file systems for differences\. 

The time that DataSync spends in the **PREPARING** phase depends on the number of files in both the source and destination file systems\. It also depends on the performance of these file systems\. The **PREPARING** phase can therefore take a few minutes to a few hours\. For more information, see [Starting your DataSync task](run-task.md)\. 

After the scanning is done and the differences are calculated, DataSync transitions to the **TRANSFERRING** phase\. At this point, DataSync starts transferring files and metadata from the source file system to the destination\. DataSync copies changes to files with contents or metadata that are different between the source and the destination\. You can narrow down the copied files by [filtering the data](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html) or by configuring DataSync to [not overwrite files that are already present in the destination](https://docs.aws.amazon.com/datasync/latest/userguide/API_Options.html#DataSync-Type-Options-OverwriteMode)\. 

**Note**  
By default, any changes to metadata on the source storage result in this metadata being copied to the destination storage\.

After the **TRANSFERRING** phase is done, DataSync verifies consistency between the source and destination file systems\. This is the **VERIFYING** phase\.

When DataSync transfers data, it always performs data\-integrity checks during the transfer\. You can enable additional verification to compare the source and destination at the end of a transfer\. This additional check can verify the entire dataset or only the files that were transferred as part of the task execution\. For most use cases, we recommend verifying only the files that were transferred\.

### How AWS DataSync verifies data integrity<a name="how-verifying-works"></a>

AWS DataSync locally calculates the checksum of every file in the source file system and the destination and compares them\. Additionally, DataSync compares the metadata of every file in the source and destination and compares them\. If there are differences in either one, verification fails with an error code that specifies precisely what failed\. For example, you might see error codes such as `Checksum failure`, `Metadata failure`, `Files were added`, `Files were removed`, and so on\. 

 For more information, see [DataSync task creation statuses](understand-task-creation-statuses.md) and **Enable verification** in the [Configuring task settings](creating-task.md#configuring-task) section\.

### How DataSync handles open and locked files<a name="open-locked-files"></a>

In general, DataSync can transfer open files without any limitations\. 

If a file is open and it's being written to during the transfer, DataSync detects data inconsistency during the **VERIFYING** phase\. This phase is when DataSync detects whether the file on the source is different from the file on the destination\. 

If a file is locked and the server prevents DataSync from opening it, DataSync skips transferring it\. DataSync logs an error during the **TRANSFERRING** phase and sends a verification error\.