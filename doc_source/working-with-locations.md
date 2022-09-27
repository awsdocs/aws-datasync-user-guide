# Working with AWS DataSync locations<a name="working-with-locations"></a>

A *location* is a storage system or service that AWS DataSync reads from or writes to\. Each DataSync transfer has a source and destination location\.

DataSync supports the following location types:
+ Network File System \(NFS\)
+ Server Message Block \(SMB\)
+ Hadoop Managed File System \(HDFS\)
+ Object storage systems
+ Amazon Elastic File System \(Amazon EFS\)
+ Amazon FSx for Windows File Server
+ Amazon FSx for Lustre
+ Amazon FSx for OpenZFS
+ Amazon FSx for NetApp ONTAP
+ Amazon S3

Where you can transfer your data depends on the following factors:
+ The source and destination locations involved in the transfer
+ If your locations belong to different AWS accounts
+ The AWS Regions involved in the transfer

## Supported transfers in the same AWS account<a name="working-with-locations-same-account"></a>

DataSync supports transfers between the following locations that belong to the same AWS account\.


| Source \(from\) | Destination \(to\) | 
| --- | --- | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 

## Supported transfers across AWS accounts<a name="working-with-locations-across-accounts"></a>

DataSync supports some transfers between storage systems in different AWS accounts\. While typically you don't need a DataSync agent for transfer between AWS services, an agent's required when these kinds of transfers only involve Amazon EFS or Amazon FSx file systems\.


| Source \(from\) | Destination \(to\) | 
| --- | --- | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html)  | 

## Supported transfers in the same AWS Region<a name="working-with-locations-same-region"></a>

There are no restrictions when transferring data within the same AWS Region \(including a Region [disabled by default](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html#rande-manage-enable)\)\. For more information, see [AWS Regions supported by DataSync](https://docs.aws.amazon.com/general/latest/gr/datasync.html)\.

## Supported transfers across AWS Regions<a name="working-with-locations-cross-regions"></a>

You can transfer data between [AWS Regions supported by DataSync](https://docs.aws.amazon.com/general/latest/gr/datasync.html) except in the following situations:
+ With AWS GovCloud \(US\) Regions, you can only transfer between AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)\.
+ You can’t transfer between Regions if one or both of the Regions is [disabled by default](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html#rande-manage-enable)\.

When you transfer data between AWS services in different AWS Regions, one of the two locations must be in the Region where you're using DataSync\.

**Important**  
You pay for data transferred between AWS Regions\. This transfer is billed as data transfer OUT from the source to destination Region\. For more information, see [Data transfer pricing](http://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)\. 