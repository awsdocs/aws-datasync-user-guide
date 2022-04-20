# Creating a location for Amazon EFS<a name="create-efs-location"></a>

A *location* for Amazon EFS is an endpoint for an Amazon EFS file system\. If you don't have an Amazon EFS file system in the current AWS Region, create one\. For information about how to create an Amazon EFS file system, see [Getting started with Amazon Elastic File System](https://docs.aws.amazon.com/efs/latest/ug/getting-started.html) in the *Amazon Elastic File System User Guide*\.

The AWS DataSync service mounts your file system from your virtual private cloud \(VPC\) using elastic network interfaces managed by the DataSync service\. DataSync fully manages the creation, the use, and the deletion of these network interfaces on your behalf\. 

**Note**  
DataSync currently doesn't support transferring files to Amazon EFS volumes that are in virtual private clouds \(VPCs\) that have dedicated tenancy\. For information about dedicated tenancy VPCs, see [Creating a VPC with an instance tenancy of dedicated](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html#creatingdedicatedvpc) in the *Amazon EC2 User Guide for Linux Instances*\. 

**To create an Amazon EFS location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Locations**\. The locations that you previously created appear in the list of locations\.

1. On the **Create location** page, choose **EFS** for ** Location type**\.

1. For **File system**, choose the **EFS file system** that you want to use as an endpoint\. You configure this location as a source or destination later\.

1. For **Mount path**, enter the mount path for your EFS file system\. The path can include a subdirectory\. If so, this is a subdirectory in the EFS file system that is used to read data from the EFS source or write data to the EFS destination\. By default, DataSync uses the root directory\. 

1. For **Subnet** and **Security Group**, DataSync automatically chooses a subnet that includes a mount target for your Amazon EFS file system and the subnet's default security group\. We recommend using these default settings\.
**Note**  
DataSync uses the security group specified in this step to connect to one of your Amazon EFS file system's mount targets on the Network File System \(NFS\) port \(2049\)\. This setup commonly works when:  
Your mount target uses the subnet's default security group\.
Your security group allows inbound port 2049 \(or "all"\) traffic from network interfaces using the same security group\.
If your mount targets or security group are configured differently than this, make sure that:  
The specified subnet includes a mount target for your Amazon EFS file system\.
Your file system's mount target accepts inbound traffic on port 2049 from network interfaces using the specified security group\.
For more information, see [Using VPC security groups for Amazon EC2 instances and mount targets](https://docs.aws.amazon.com/efs/latest/ug/network-access.html) in the *[Amazon Elastic File System User Guide](https://docs.aws.amazon.com/efs/latest/ug/)*\.

1. \(Optional\) Provide values for the **Key** and **Value** fields to tag the EFS file system\. A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. We recommend using tags for naming your resources\. 

1. When you are done, choose **Create location**\. The location that you just created appears in the list of locations\.

## Considerations when creating a location for Amazon EFS<a name="efs-considerations"></a>

Be sure to consider the following when creating a location for Amazon EFS:
+ When you create an Amazon EFS file system in Bursting Throughput mode, you get an allocation of 2\.1\-TB worth of burst credits\. All Amazon EFS file systems are able to burst up to 100 MB per second of throughput when using Bursting Throughput mode\. File systems with more than 1 TiB of S3 Standard class storage can drive 100 MiB per second per TB when burst credits are available\.

  DataSync consumes file system burst credits\. This can have an impact on the performance of your applications\. When using DataSync with a file system that has an active workload, consider using EFS Provisioned Throughput\.
+ Amazon EFS file systems that are in General Purpose performance mode have a limit of 35,000 file system operations per second\. This limit can impact the maximum throughput DataSync can achieve when copying files\.

  Operations that read data or metadata consume one file operation, and operations that write data or update metadata consume five file operations\. This means that a file system can support 35,000 read operations per second, or 7,000 write operations, or some combination of the two\. File operations are counted from all connecting clients\. 

  For more information, see [Amazon EFS performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html) in the *Amazon Elastic File System User Guide*\.