# Creating an Amazon EFS location<a name="create-efs-location"></a>

An AWS DataSync *location* is an endpoint for an Amazon EFS file system\.

## Accessing Amazon EFS file systems<a name="create-efs-location-access"></a>

DataSync mounts your Amazon EFS file system as the root user from your virtual private cloud \(VPC\) using [network interfaces](datasync-network.md#required-network-interfaces)\.

When creating your location, you specify the subnet and security groups that DataSync uses to connect to one of your Amazon EFS file system's mount targets or [access points](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html) using Network File System \(NFS\) port 2049\.

DataSync can also mount Amazon EFS file systems configured for restricted access\. For example, you can specify an AWS Identity and Access Management \(IAM\) role that gives DataSync the necessary level of permission to connect to your file system\. For more information, see [Using IAM policies to access your Amazon EFS file system](#create-efs-location-iam)\.

## Considerations with Amazon EFS locations<a name="efs-considerations"></a>

Think about the following when creating a DataSync location for an Amazon EFS file system:
+ DataSync doesn't support transferring files to Amazon EFS file system volumes in VPCs with dedicated tenancy\. For more information, see [Creating a VPC with an instance tenancy of dedicated](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html#creatingdedicatedvpc) in the *Amazon EC2 User Guide for Linux Instances*\. 
+ When you create an Amazon EFS file system in Bursting Throughput mode, you get an allocation of 2\.1\-TB worth of burst credits\. All Amazon EFS file systems can burst up to 100 MB per second of throughput with Bursting Throughput mode\. File systems with more than 1 TiB of Amazon S3 Standard class storage can drive 100 MiB per second per TB when burst credits are available\.

  DataSync consumes file system burst credits\. This can have an impact on the performance of your applications\. When using DataSync with a file system that has an active workload, consider using EFS Provisioned Throughput\.
+ Amazon EFS file systems that are in General Purpose performance mode have a limit of 35,000 file system operations per second\. This limit can impact the maximum throughput DataSync can achieve when copying files\.

  Operations that read data or metadata consume one file operation\. Operations that write data or update metadata consume five file operations\. This means a file system can support 35,000 read operations per second, 7,000 write operations, or some combination of the two\. File operations are counted from all connecting clients\. 

  For more information, see [Amazon EFS performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html) in the *Amazon Elastic File System User Guide*\.

## Creating the location<a name="create-efs-location-how-to"></a>

To create the location, you need an existing Amazon EFS file system\. If you don't have one, see [Getting started with Amazon Elastic File System](https://docs.aws.amazon.com/https://docs.aws.amazon.com/efs/latest/ug/getting-started.html) in the *Amazon Elastic File System User Guide*\.

**To create an Amazon EFS location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**, and then choose **Create location**\.

1. For ** Location type**, choose **Amazon EFS file system**\.

   You configure this location as a source or destination later\. 

1. For **File system**, choose the Amazon EFS file system that you want to use as a location\.

   You configure this location as a source or destination later\.

1. For **Mount path**, enter a mount path for your Amazon EFS file system\.

   This specifies where DataSync reads or writes data \(depending on if this is a source or destination location\)\.

   By default, DataSync uses the root directory \(or access point if you configure one\)\. You can also specify subdirectories using forward slashes \(for example, `/path/to/directory`\)\.

1. For **Subnet** choose a subnet where DataSync creates the network interfaces for managing traffic during your transfer\.

   The subnet must be located:
   + In the same VPC as the Amazon EFS file system\.
   + In the same Availability Zone as at least one file system mount target\.
**Note**  
You don't need to specify a subnet that includes a file system mount target\.

1. For **Security groups**, choose the security groups associated with an Amazon EFS file system's mount target\.
**Note**  
The security groups that you specify must allow inbound traffic on NFS port 2049\. For more information, see [Using VPC security groups for Amazon EC2 instances and mount targets](https://docs.aws.amazon.com/efs/latest/ug/network-access.html) in the *[Amazon Elastic File System User Guide](https://docs.aws.amazon.com/efs/latest/ug/)*\.

1. For **In\-transit encryption**, choose whether you want DataSync to use Transport Layer Security \(TLS\) encryption when it copies data to or from your file system\.
**Note**  
You must enable this setting if you want to configure an access point, IAM role, or both with your location\.

1. \(Optional\) For **EFS access point**, choose an access point that DataSync can use to mount your Amazon EFS file system\.

1. \(Optional\) For **IAM role**, specify a role that allows DataSync to access your file system\.

   For information on creating this role, see [Using IAM policies to access your Amazon EFS file system](#create-efs-location-iam)

1. \(Optional\) Select **Add tag** to tag your file system\.

   A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. 

1. Choose **Create location**\.

## Using IAM policies to access your Amazon EFS file system<a name="create-efs-location-iam"></a>

You can configure your Amazon EFS file system with a higher level of security by using IAM policies\. In your [file system policy](#create-efs-location-iam-policy), you can specify an IAM role that still allows DataSync to connect with the file system\.

**Note**  
To use an IAM role, you must enable TLS for in\-transit encryption when creating a DataSync location for your file system\.

For more information, see [Using IAM to control file system data access](https://docs.aws.amazon.com/efs/latest/ug/iam-access-control-nfs-efs.html) in the *Amazon Elastic File System User Guide*\.

### Creating an IAM role for DataSync<a name="create-efs-location-iam-role"></a>

Create a role with DataSync as the trusted entity\.

**To create the IAM role**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the left navigation pane, under **Access management**, choose **Roles**, and then choose **Create role**\.

1. On the **Select trusted entity** page, for **Trusted entity type**, choose **Custom trust policy**\.

1. Paste the following JSON into the policy editor:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [{
           "Effect": "Allow",
           "Principal": {
               "Service": "datasync.amazonaws.com"
           },
           "Action": "sts:AssumeRole"
       }]
   }
   ```

1. Choose **Next**\. On the **Add permissions** page, choose **Next**\.

1. Give your role a name and choose **Create role**\.

Specify this role when creating the location for your Amazon EFS file system\.

### Example Amazon EFS file system policy<a name="create-efs-location-iam-policy"></a>

The following sample IAM policy includes elements that help restrict access to an Amazon EFS file system \(identified in the policy as `fs-1234567890abcdef0`\):
+ `Principal`: Specifies an IAM role that gives DataSync permission to connect to the file system\.
+ `Action`: Gives DataSync root access and allows it to read from and write to the file system\.
+ `aws:SecureTransport`: Requires NFS clients to use TLS when connecting to the file system\.
+ `elasticfilesystem:AccessPointArn`: Allows access to the file system only through a specific access point\.

```
{
    "Version": "2012-10-17",
    "Id": "ExampleEFSFileSystemPolicy",
    "Statement": [{
        "Sid": "AccessEFSFileSystem",
        "Effect": "Allow",
        "Principal": {
            "AWS": "arn:aws:iam::111122223333:role/MyDataSyncRole"
        },
        "Action": [
            "elasticfilesystem:ClientMount",
            "elasticfilesystem:ClientWrite",
            "elasticfilesystem:ClientRootAccess"
        ],
        "Resource": "arn:aws:elasticfilesystem:us-east-1:111122223333:file-system/fs-1234567890abcdef0",
        "Condition": {
            "Bool": {
                "aws:SecureTransport": "true"
            },
            "StringEquals": {
                "elasticfilesystem:AccessPointArn": "arn:aws:elasticfilesystem:us-east-1:111122223333:access-point/fsap-abcdef01234567890"
            }
        }
    }]
}
```