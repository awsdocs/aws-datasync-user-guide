# Working with locations<a name="working-with-locations"></a>

In this section, you can find information about how to create and configure locations\. A *location* defines the storage system or service that you want to read data from or write data to\. AWS DataSync supports the following location types:
+ Network File System \(NFS\)
+ Server Message Block \(SMB\)
+ Hadoop Managed File System \(HDFS\)
+ On\-premises \(self\-managed\) object storage
+ Amazon Elastic File System \(Amazon EFS\)
+ Amazon FSx for Windows File Server
+ Amazon FSx for Lustre
+ Amazon FSx for OpenZFS
+ Amazon S3

When you create a task that transfers data between AWS services in different AWS Regions, one of the two locations that you specify must reside in the Region where DataSync is being used\. The other location must be specified in a different Region\.

You can transfer data between AWS Regions, except for the China Regions and the AWS GovCloud \(US\) Regions\. You can also transfer data between the AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\) Regions\.

DataSync supports the following source and destination location combinations\. 

**Note**  
In the following tables, AWS Regions indicates Regions other than the China Regions and the AWS GovCloud \(US\) Regions\. Transfers involving the AWS GovCloud \(US\) Regions can only be between the AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\) Regions\. 


| Source \(from\) | Destination \(to\) | 
| --- | --- | 
|  Self\-managed storage \(including NFS shares, SMB shares, HDFS, object storage, or NFS on your AWS Snowcone\)  |  Amazon S3 \(in AWS Regions\), Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  | 
|  Amazon S3 \(in AWS Regions\), Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  |  Self\-managed storage \(including NFS shares, SMB shares, HDFS, object storage, or NFS on your AWS Snowcone\)  | 
|  Amazon S3 \(in AWS Regions\), Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  |  Amazon S3 \(in AWS Regions\), Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  | 
|  Amazon S3 \(in AWS Regions\)  |  Amazon S3 on AWS Outposts  | 
|  Amazon S3 on AWS Outposts  |  Amazon S3 \(in AWS Regions\)  | 

In addition, you can use the following combinations to transfer data between managed file systems and Amazon S3 buckets in different AWS accounts\. When these kinds of transfers only involve Amazon EFS or supported Amazon FSx file systems, you must use a DataSync agent\.


| Source \(from\) | Destination \(to\) | 
| --- | --- | 
|  Amazon EFS \(configured as an NFS location\) or FSx for Windows File Server \(configured as an SMB location\)  |  Amazon S3 \(in AWS Regions\), Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  | 
|  Amazon S3 \(in AWS Regions\)  |  Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  | 
|  Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS  |  Amazon S3 \(in AWS Regions\)  | 

**Important**  
When you use DataSync to copy files or objects between AWS Regions, you pay for data transfer between Regions\. This transfer is billed as data transfer OUT from your source Region to your destination Region\. For more information, see [Data transfer pricing](http://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)\. 

**Topics**
+ [Creating a location for NFS](create-nfs-location.md)
+ [Creating a location for SMB](create-smb-location.md)
+ [Creating a location for HDFS](create-hdfs-location.md)
+ [Creating a location for object storage](create-object-location.md)
+ [Creating a location for Amazon EFS](create-efs-location.md)
+ [Creating a location for FSx for Windows File Server](create-fsx-location.md)
+ [Creating a location for FSx for Lustre](create-lustre-location.md)
+ [Creating a location for FSx for OpenZFS](create-openzfs-location.md)
+ [Creating a location for Amazon S3](create-s3-location.md)
+ [How DataSync handles metadata and special files](special-files.md)
+ [Deleting a location](deleting-location.md)