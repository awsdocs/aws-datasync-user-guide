# How AWS DataSync works<a name="how-datasync-works"></a>

Get a visual overview of how AWS DataSync works and learn key concepts to help you move your data quickly\.

## DataSync architecture<a name="datasync-archtecture"></a>

**Topics**
+ [Transferring between on\-premises storage and AWS](#onprem-aws)
+ [Transferring between AWS storage services](#in-cloud-transfer)
+ [Transferring between cloud storage systems and AWS storage services](#ec2-agent-in-region)

The following diagrams show how and where DataSync commonly transfers storage data\. 

For a full list of DataSync supported storage systems and services, see [Working with AWS DataSync locations](working-with-locations.md)\.

### Transferring between on\-premises storage and AWS<a name="onprem-aws"></a>

The following diagram shows a high\-level overview of DataSync transferring files between self\-managed, on\-premises storage systems and AWS services\.

![\[An overview of a common DataSync scenario where data transfers from an on-premises storage system to a supported AWS storage resource (such as an Amazon S3 bucket or Amazon EFS file system).\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/DataSync-chart-on-prem.png)

The diagram illustrates a common DataSync use case:
+ A DataSync agent copying data from an on\-premises storage system\.
+ Data moving into AWS via Transport Layer Security \(TLS\)\.
+ DataSync copying data to a supported AWS storage service\.

### Transferring between AWS storage services<a name="in-cloud-transfer"></a>

The following diagram shows a high\-level overview of DataSync transferring files between AWS services in the same AWS account\.

![\[An overview of a common DataSync scenario where data transfers between AWS storage resources (such as an Amazon S3 bucket or Amazon EFS file system).\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/DataSync-chart-agentless.png)

The diagram illustrates a common DataSync use case:
+ DataSync copying data from a supported AWS storage service\.
+ Data moving across AWS Regions via TLS\.
+ DataSync copying data to a supported AWS storage service\. 

When transferring between AWS storage services \(whether in the same AWS Region or across AWS Regions\), your data remains in the AWS network and doesn't traverse the public internet\.

**Important**  
You pay for data transferred between AWS Regions\. This is billed as data transfer OUT from your source Region to your destination Region\. For more information, see [Data transfer pricing](http://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)\.

### Transferring between cloud storage systems and AWS storage services<a name="ec2-agent-in-region"></a>

With DataSync, you can transfer data between cloud storage systems and AWS services\. In this context, cloud storage systems can include:
+ Self\-managed storage systems hosted by AWS \(for example, an NFS share in your virtual private cloud within AWS\)\.
+ Storage systems or services hosted by another cloud provider\.

For more information, see the following topics:
+ [Deploying your DataSync agent in an AWS Region](using-ec2-agent-in-region.md)
+ [Tutorial: Transferring data from Google Cloud Storage to Amazon S3](tutorial_transfer-google-cloud-storage.md)

## Concepts and terminology<a name="terminology"></a>

Familiarize yourself with DataSync features\.

### Agent<a name="sync-agents"></a>

An *agent* is a virtual machine \(VM\) that you own that's used to read or write data from storage systems\. The agent can be deployed on VMware ESXi, Linux Kernel\-based Virtual Machine \(KVM\), Microsoft Hyper\-V hypervisors, or it can be launched as an Amazon EC2 instance\. You use the DataSync console, AWS CLI, or DataSync API to set up and activate your agent\. The activation process associates your agent VM with your AWS account\. For information about agents, see [Working with AWS DataSync agents](working-with-agents.md)\.

### Location<a name="sync-locations"></a>

A *location* identifies where you're copying data from or to\. Each DataSync transfer \(also known as a *task*\) has a source and destination location\. For more information, see [Working with AWS DataSync locations](working-with-locations.md)\.

### Task<a name="tasks"></a>

A *task* describes a DataSync transfer\. It identifies a source and destination location along with details about how to copy data between those locations\. You also can specify how a task treats metadata, deleted files, and permissions\.

### Task execution<a name="task-executions"></a>

A *task execution* is an individual run of a DataSync task\. There are several phases involved in a task execution\. For more information, see [Task execution statuses](working-with-task-executions.md#understand-task-execution-statuses)\.

## How DataSync transfers files and objects<a name="transfering-files"></a>

**Topics**
+ [How DataSync verifies data integrity](#how-verifying-works)
+ [How DataSync handles open and locked files](#open-locked-files)

When you start a transfer, DataSync examines your source and destination storage systems to determine what to sync\. It does this by recursively scanning the contents and metadata of both systems to identify differences between the two\. This can take just minutes or a few hours depending on the number of files or objects involved \(including the performance of the storage systems\)\.

DataSync then begins moving your data \(including metadata\) from the source to destination based on [how you set up the transfer](create-task.md)\. For example, DataSync always performs data\-integrity checks during a transfer\. When the transfer's complete, DataSync can also verify the entire dataset between locations or just the data you copied\. \(In most cases, we recommend verifying only what was transferred\.\) There are options for filtering what to transfer, too\.

### How DataSync verifies data integrity<a name="how-verifying-works"></a>

DataSync locally calculates the checksum of every file or object in the source and destination storage systems and compares them\. Additionally, DataSync compares the metadata of every file or object in the source and destination\. If there are differences in either one, verification fails with an error code that specifies precisely what failed\. For example, you might see error codes such as `Checksum failure`, `Metadata failure`, `Files were added`, `Files were removed`, and so on\. 

For more information, see [Data verification options](create-task.md#configure-data-verification-options)\.

### How DataSync handles open and locked files<a name="open-locked-files"></a>

Keep in mind the following when trying to transfer files that are in use or locked:
+ In general, DataSync can transfer open files without any limitations\.
+ If a file is open and being written to during a transfer, DataSync can detect this kind of inconsistency during the transfer task's verification phase\. To get the latest version of the file, you must run the task again\.
+ If a file is locked and the server prevents DataSync from opening it, DataSync skips the file during the transfer and logs an error\.
+ DataSync can't lock or unlock files\.