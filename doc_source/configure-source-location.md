# Configure a source location<a name="configure-source-location"></a>

A *task* consists of a pair of locations that data will be transferred between\. The *source location* defines the storage system or service that you want to read data from\. The *destination location* defines the storage system or service that you want to write data to\.

For a list of all DataSync supported source and destination endpoints, see [Working with locations](working-with-locations.md)\.

In the following walkthrough, we give an example of configuring a Network File System \(NFS\) file system as the source location\. 

To configure a different location type as your source location, see the following topics:
+ [Creating a location for NFS](create-nfs-location.md)
+ [Creating a location for SMB](create-smb-location.md)
+ [Creating a location for HDFS](create-hdfs-location.md)
+ [Creating a location for object storage](create-object-location.md)
+ [Creating a location for Amazon EFS](create-efs-location.md)
+ [Creating a location for FSx for Windows File Server](create-fsx-location.md)
+ [Creating a location for FSx for Lustre](create-lustre-location.md)
+ [Creating a location for FSx for OpenZFS](create-openzfs-location.md)
+ [Creating a location for Amazon S3](create-s3-location.md)

**To create an NFS location**

1. On the **Configure source location** page, choose **Create a new location** or **Choose existing location**\. **Create a new location** enables you to define a new location and **Choose existing location** enables you to choose from locations that you have previously created in this AWS Region\.  


1. For **Location type** in the **Configuration** section, choose your NFS server from the list\.

1. For **Agents**, choose your agent from the list\. You can add more than one agent\. For this walkthrough, we add only one agent\.
**Note**  
In many cases, you might be transferring from an in\-cloud NFS file system or an Amazon EFS file system\. In such cases, make sure that you choose an agent that you created in an Amazon EC2 instance that can access this file system\.  
You can't use agents that are created with different endpoint types for the same task\.

1. For **NFS server**, enter the IP address or domain name of your NFS server\. An agent that's installed on\-premises uses this hostname to mount the NFS server in a network\. The NFS server should allow full access to all files\.

1. For **Mount path**, enter a path that's exported by the NFS server, or a subdirectory that can be mounted by other NFS clients in your network\. The path is used to read data from or write data to your NFS server\.

1. Choose **Next** to open the **Configure destination location** page\.