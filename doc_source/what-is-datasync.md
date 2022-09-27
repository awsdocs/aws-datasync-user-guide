# What is AWS DataSync?<a name="what-is-datasync"></a>

AWS DataSync is an online data transfer service that simplifies, automates, and accelerates moving data between storage systems and services\.

DataSync can copy data to and from:
+ Network File System \(NFS\) file servers
+ Server Message Block \(SMB\) file servers
+ Hadoop Distributed File System \(HDFS\)
+ Object storage systems
+ Amazon Simple Storage Service \([Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html)\) buckets
+ [Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/) file systems
+ [Amazon FSx for Windows File Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/) file systems
+ [Amazon FSx for Lustre](https://docs.aws.amazon.com/fsx/latest/LustreGuide/what-is.html) file systems
+ [Amazon FSx for OpenZFS](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/what-is.html) file systems
+ [Amazon FSx for NetApp ONTAP](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/what-is-fsx-ontap.html) file systems
+ AWS Snowcone devices

## Use cases<a name="use-cases"></a>

These are some of the main use cases for DataSync:
+ **Data migration** – Move active datasets rapidly over the network into Amazon S3, Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS\. DataSync includes automatic encryption and data integrity validation to help make sure that your data arrives securely, intact, and ready to use\.
+ **Archiving cold data** – Move cold data stored in on\-premises storage directly to durable and secure long\-term storage classes such as S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive\. Doing so can free up on\-premises storage capacity and shut down legacy systems\. 
+ **Data protection** – Move data into any Amazon S3 storage class, choosing the most cost\-effective storage class for your needs\. You can also send data to Amazon EFS, FSx for Windows File Server, FSx for Lustre, or FSx for OpenZFS for a standby file system\.
+ **Data movement for timely in\-cloud processing** – Move data in or out of AWS for processing\. This approach can speed up critical hybrid cloud workflows across many industries\. These include machine learning in the life\-sciences industry, video production in media and entertainment, big\-data analytics in financial services, and seismic research in the oil and gas industry\.

## Benefits<a name="benefits"></a>

By using AWS DataSync, you can get the following benefits:
+ **Simplify and automate data movement** – DataSync makes it easier to move data over the network between storage systems and services\. DataSync automates both the management of data\-transfer processes and the infrastructure required for high performance and secure data transfer\.
+ **Transfer data securely** – DataSync provides end\-to\-end security, including encryption and integrity validation, to help ensure that your data arrives securely, intact, and ready to use\. DataSync accesses your AWS storage through built\-in AWS security mechanisms, such as AWS Identity and Access Management \(IAM\) roles\. It also supports virtual private cloud \(VPC\) endpoints, giving you the option to transfer data without traversing the public internet and further increasing the security of data copied online\.
+ **Move data faster** – Transfer data rapidly over the network into AWS\. DataSync uses a purpose\-built network protocol and a parallel, multi\-threaded architecture to accelerate your transfers\. This approach speeds up migrations, recurring data\-processing workflows for analytics and machine learning, and data\-protection processes\.
+ **Reduce operational costs** – Move data cost\-effectively with the flat, per\-gigabyte pricing of DataSync\. Save on script development and deployment and maintenance costs\. Avoid the need for costly commercial transfer tools\.

## Additional resources<a name="first-time-user"></a>

We recommend that you read the following:
+ [DataSync resources](http://aws.amazon.com/datasync/resources/) – Includes blogs, videos, and other training materials
+ [AWS re:Post](https://repost.aws/) – See the latest discussion around DataSync
+ [AWS DataSync pricing](http://aws.amazon.com/datasync/pricing) – DataSync pricing information

DataSync also supports Terraform\. To learn more about DataSync deployment automation with Terraform, see the [Terraform documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/datasync_agent)\.