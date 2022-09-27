# Deploying your DataSync agent in an AWS Region<a name="using-ec2-agent-in-region"></a>

The following guidance can help with common scenarios if you deploy an AWS DataSync agent in an AWS Region\. If you don't have an agent yet, see [Deploy your agent as an Amazon EC2 instance](deploy-agents.md#ec2-deploy-agent)\.

## Transferring data from a cloud file system to another cloud file system or Amazon S3<a name="efs-efs"></a>

To transfer data between AWS accounts, or from a cloud file system, the DataSync agent must be located in the same AWS Region and AWS account where the source file system resides\. This type of transfer includes the following:
+ Transfers between Amazon EFS or FSx for Windows File Server file systems to AWS storage in a different AWS account\.
+ Transfers from self\-managed file systems to AWS storage services\.

**Important**  
Deploy your agent such that it doesn't require network traffic between Availability Zones \(to avoid charges for such traffic\)\.   
To access your Amazon EFS or FSx for Windows File Server file system, deploy the agent in an Availability Zone that has a mount target to your file system\.
For self\-managed file systems, deploy the agent in the Availability Zone where your file system resides\.
To learn more about data transfer prices for all AWS Regions, see [Amazon EC2 On\-Demand pricing](http://aws.amazon.com/ec2/pricing/on-demand/)\. 

For example, the following diagram shows a high\-level view of the DataSync architecture for transferring data from in\-cloud Network File System \(NFS\) to in\-cloud NFS or Amazon S3\. 

![\[Diagram showing data transfer between source Region containing a virtual private cloud (VPC) with an EFS file system and DataSync agent, and a destination Region with a DataSync endpoint and EFS file system.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/efs-efs-ec2.png)

**Note**  
Deploy the agent in the AWS Region and AWS account where the source file system resides\.  
When you're copying between two Amazon EFS file systems in different AWS accounts, we recommend that you use the NFS \(source\) to EFS \(destination\) transfer\.
When you're copying between two Amazon FSx file systems in different AWS accounts, we recommend that you use the Server Message Block \(SMB\) \(source\) to Amazon FSx \(destination\) transfer\.

## Transferring data from Amazon S3 to cloud file systems<a name="s3-cloud-nfs"></a>

The following diagram provides a high\-level view of the DataSync architecture for transferring data from Amazon S3 to an in\-cloud file system\. You can use this architecture to transfer data from one AWS account to another, or to transfer data from Amazon S3 to a self\-managed in\-cloud file system\. 

![\[Diagram showing data transfer between source Region containing an S3 bucket and DataSync endpoint, and a destination Region containing a VPC with an EFS file system and DataSync agent.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/s3-efs-ec2.png)