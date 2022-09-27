# Understanding your storage with AWS DataSync Discovery<a name="understanding-your-storage"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

AWS DataSync Discovery helps you accelerate your migration to AWS\. With DataSync Discovery, you can do the following:
+ **Understand how your on\-premises storage is used** – DataSync Discovery provides detailed reporting about your storage system resources, including utilization, capacity, and configuration information\.
+ **Get recommendations about migrating your data to AWS** – DataSync Discovery can suggest AWS storage services \(such as Amazon FSx for NetApp ONTAP, Amazon EFS, and Amazon FSx for Windows File Server\) for your data\. Recommendations include a cost estimate and help you understand how to configure a suggested storage service\. When you're ready, you can then use DataSync to migrate your data to AWS\.

## How does DataSync Discovery work?<a name="how-discovery-works"></a>

Learn the key concepts and terminology related to DataSync Discovery\.

### Agent<a name="how-discovery-works-agent"></a>

An *agent* is a virtual machine \(VM\) or Amazon EC2 instance that you deploy and manage\. DataSync Discovery uses an agent to access the management interface of your on\-premises storage system and report findings to AWS\.

For more information, see [Create an agent](discovery-getting-started.md#discovery-create-agent)\.

### Discovery job<a name="how-discovery-works-job"></a>

You run a *discovery job* to collect information about your on\-premises storage system through the storage system's management interface\.

You can run a discovery job between 1 hour and 31 days\. You'll get more accurate AWS storage recommendations the longer your discovery job runs\.

For more information, see [Working with DataSync discovery jobs](discovery-job-create.md)\.

### Storage system resource information<a name="how-discovery-works-perf"></a>

DataSync Discovery can give you performance and utilization information about your on\-premises storage system's resources\. For example, get an idea about how much storage capacity is being used in a specific storage volume compared to how much capacity that you originally provisioned\.

You can view this information as it's added and updated by using the following:
+ The DataSync console
+ The [DescribeStorageSystemResources](discovery-api-actions.md#discovery-describestoragesystemresources) operation
+ The [DescribeStorageSystemResourceMetrics](discovery-api-actions.md#discovery-describestoragesystemresourcemetrics) operation

For more information, see [Storage resource information collected by AWS DataSync Discovery](discovery-understand-findings.md)\.

### AWS storage recommendations<a name="how-discovery-works-recs"></a>

Using the information that it collects about your on\-premises storage system's resources, DataSync Discovery recommends AWS storage services to help plan your migration to AWS\.

You can view recommendations by using the following:
+ The DataSync console
+ The [DescribeStorageSystemResources](discovery-api-actions.md#discovery-describestoragesystemresources) operation

For more information, see [Recommendations provided by AWS DataSync Discovery](discovery-understand-recommendations.md)\.

## DataSync Discovery architecture<a name="discovery-architecture"></a>

The following diagram illustrates how DataSync Discovery collects information and provides recommendations for migrating data from an on\-premises storage system to AWS\.

![\[The first connection is for communicating with the source storage location. The second connection is for transferring between locations. The third and final connection is with the destination storage location.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/datasync-discovery-overview-diagram.png)


| Reference | Description | 
| --- | --- | 
| 1 | A DataSync agent connects to your on\-premises storage system's management interface \(using port 443, for example\)\. You then run a discovery job to collect information about your system\. | 
| 2 | The agent sends the information that it collects to DataSync Discovery\. | 
| 3 | Using the information that it collects, DataSync Discovery recommends AWS storage services that you can migrate your data to\. | 

## Data protection<a name="discovery-data-protection"></a>

DataSync Discovery stores and manages the data that it collects about your on\-premises storage system for up to 60 days\. When you remove an on\-premises storage system resource from DataSync Discovery, you permanently delete any associated discovery jobs, collected data, and recommendations\.

## Limitations<a name="discovery-quotas"></a>
+ You can currently use DataSync Discovery only in the US East \(N\. Virginia\) Region \(`us-east-1`\)\.
+ DataSync Discovery only supports public service endpoints at this time\.
+ You can add up to 10 storage systems per AWS account and AWS Region\.
+ A DataSync agent can access up to four storage systems at a time\.