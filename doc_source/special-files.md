# How DataSync handles metadata and special files<a name="special-files"></a>

AWS DataSync saves metadata and special files \(links and directories\) when copying data to and from storage systems and services\.

However, DataSync doesn't copy system\-level settings\. For example, when copying objects, DataSync doesn't copy your storage system's encryption setting\. If you're copying from an SMB share, DataSync doesn't copy the permissions you configured at the file system level\.

## Metadata copied by DataSync<a name="metadata-copied"></a>

How DataSync maintains metadata depends on what storage systems are involved in your transfer\.

**Topics**
+ [Metadata copied between systems with a similar metadata structure](#metadata-copied-similar)
+ [Metadata copied between systems with a different metadata structure](#metadata-copied-different)
+ [Default POSIX metadata applied by DataSync](#POSIX-metadata)

### Metadata copied between systems with a similar metadata structure<a name="metadata-copied-similar"></a>

DataSync preserves metadata between storage systems that have a similar metadata structure\.

**When copying between self\-managed Network File System \(NFS\), Amazon FSx for Lustre, Amazon FSx for OpenZFS, Amazon FSx for NetApp ONTAP \(using NFS\), or Amazon EFS, and Amazon EFS, FSx for Lustre, FSx for OpenZFS, or FSx for ONTAP \(using NFS\)** – In this case, DataSync can copy the following metadata:
+ File and folder modification timestamps
+ File and folder access timestamps \(DataSync can only do this on a best\-effort basis\)
+ User ID \(UID\) and group ID \(GID\)
+ POSIX permissions

**When copying between Hadoop Distributed File System \(HDFS\) and Amazon EFS, FSx for Lustre, FSx for OpenZFS, or FSx for ONTAP \(using NFS\)** – In this case, DataSync can copy the following metadata:
+ File and folder modification timestamps
+ File and folder access timestamps \(DataSync can only do this on a best\-effort basis\)
+ POSIX permissions

**Note**  
HDFS uses strings to store file and folder user and group ownership, rather than numeric identifiers \(such as UIDs and GIDs\)\. When copying from HDFS to Amazon EFS, FSx for Lustre, FSx for OpenZFS, or FSx for ONTAP \(using NFS\), default values for UIDs and GIDs are applied on the destination file system\. For more information about default values, see [Default POSIX metadata applied by DataSync](#POSIX-metadata)\.

**When copying between self\-managed Server Message Block \(SMB\), Amazon FSx for Windows File Server, or FSx for ONTAP \(using SMB\), and FSx for Windows File Server or FSx for ONTAP \(using SMB\)** – In this case, DataSync can copy the following metadata:
+ File timestamps: access time, modification time, and creation time
+ File owner security identifier \(SID\)
+ Standard file attributes:
  + Read\-only \(R\)
  + Archive \(A\)
  + System \(S\)
  + Hidden \(H\)
  + Compressed \(C\)
  + Not content indexed \(N\)
  + Encrypted \(E\)
  + Temporary \(T\)
  + Offline \(O\)
  + Sparse \(P\)
**Note**  
DataSync attempts to copy the archive, compressed, and sparse attributes\. If these attributes aren't applied on the destination, they're ignored during task verification\.
+ NTFS discretionary access lists \(DACLs\), which determine whether to grant access to an object
+ NTFS system access control lists \(SACLs\), which are used by administrators to log attempts to access a secured object
**Note**  
Copying DACLs and SACLs requires granting specific permissions to the Windows user that DataSync uses to access your location using SMB\. For more information, see creating a location for [SMB](create-smb-location.md#configuring-smb), [FSx for Windows File Server](create-fsx-location.md), or [FSx for ONTAP](create-ontap-location.md) \(depending on the type of location in your transfer\)\.

**When copying between self\-managed NFS, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), or Amazon EFS and Amazon S3** – In this case, the following metadata is stored as Amazon S3 user metadata:
+ File and folder modification timestamps
+ File and folder access timestamps \(DataSync can only do this on a best\-effort basis\)
+ User ID and group ID
+ POSIX permissions

The file metadata stored in Amazon S3 user metadata is interoperable with NFS shares on file gateways using AWS Storage Gateway\. A file gateway enables low\-latency access from on\-premises networks to data that was copied to Amazon S3 by DataSync\. This metadata is also interoperable with FSx for Lustre\.

When DataSync copies objects that contain this metadata back to an NFS server, the file metadata is restored\. Restoring metadata requires granting elevated permissions to the NFS server\. For more information, see [Creating an NFS location](create-nfs-location.md)\.

**When copying between HDFS and Amazon S3** – In this case, the following metadata is stored as Amazon S3 user metadata:
+ File and folder modification timestamps
+ File and folder access timestamps \(DataSync can only do this on a best\-effort basis\)
+ User name and group name
+ POSIX permissions

**Note**  
HDFS uses strings to store file and folder user and group ownership, rather than numeric identifiers, such as UIDs and GIDs\. DataSync ignores user and group name metadata values stored in Amazon S3 when copying to Amazon EFS or self\-managed NFS\.

**When copying between object storage systems and Amazon S3 or between two Amazon S3 buckets** – In this case, DataSync only copies user\-defined metadata and tags\. DataSync doesn't copy other object information, such as object access control lists \(ACLs\) or prior object versions\.

**Important**  
If you're transferring objects from a Google Cloud Storage bucket, copying object tags may cause your DataSync task to fail\. To prevent this, deselect the **Copy object tags** option when configuring your task settings\. For more information, see [File metadata and management options](create-task.md#configure-file)\.

### Metadata copied between systems with a different metadata structure<a name="metadata-copied-different"></a>

When copying between storage systems that don't have a similar metadata structure, DataSync sets metadata using the following rules\.


| If you copy this way | This happens to metadata | 
| --- | --- | 
|  From an SMB share to Amazon EFS, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), or Amazon S3  From FSx for Windows File Server or FSx for ONTAP \(using SMB\) to an NFS share or HDFS  |  Default POSIX metadata is set for all files and folders on the target NFS server, Amazon EFS file system, FSx for Lustre file system, FSx for OpenZFS file system, or FSx for ONTAP file system, or stored in the Amazon S3 object's metadata\. This approach includes using the default POSIX user ID and group ID values\. On HDFS, file and folder timestamps are applied from the source\. The file or folder owner is set based on the user or Kerberos principal specified in DataSync\. The Groups Mapping configuration on the Hadoop cluster determines the group\.  | 
|  From an NFS share or HDFS to FSx for Windows File Server or FSx for ONTAP \(using SMB\) From Amazon EFS, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), or Amazon S3 to an SMB share  |  File and folder timestamps are applied from the source\. Ownership is set based on the Windows user that was specified in DataSync to access the Amazon FSx or SMB share\. Permissions are inherited from the parent directory\.  | 

### Default POSIX metadata applied by DataSync<a name="POSIX-metadata"></a>

When your source and destination locations don't have a similar metadata structure, or when source metadata is missing, DataSync applies default POSIX metadata\.

This is how DataSync applies default POSIX metadata specifically in these situations:
+ When transferring files from an Amazon S3 or object storage location to an Amazon EFS, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), NFS, or HDFS location, in cases where Amazon S3 objects don't have DataSync POSIX metadata
+ When transferring from an SMB location to an NFS, HDFS, Amazon S3, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), or Amazon EFS location

The following table shows the default POSIX metadata and permissions that DataSync applies\.


| Permission | Value | 
| --- | --- | 
|  UID  |  65534  | 
|  GID  |  65534  | 
|  Folder Permission  |  0755  | 
|  File Permission  |  0644  | 

HDFS stores file and folder user and group ownership using strings, rather than numeric identifiers, such as UIDs and GIDs\. When there is no equivalent metadata on the source location, file and folder ownership is set based on the user or Kerberos principal that you specified in DataSync\. The group is determined by the Groups Mapping configuration on the Hadoop cluster\. 

## Links and directories copied by DataSync<a name="special-files-copied"></a>

DataSync handles copied hard links, symbolic links, and directories differently depending on the storage locations you're using\.

**Hard links**  
**When copying between an NFS server, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), and Amazon EFS**, hard links are preserved\.  
**When copying to Amazon S3**, each hard link is transferred only once\. Separate Amazon S3 objects are created for each copy\. If a hard link is unchanged in Amazon S3, it's correctly restored upon transfer to an NFS server, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), or Amazon EFS\.  
**When copying between an SMB file share, FSx for Windows File Server, and FSx for ONTAP \(using SMB\)**, hard links aren't supported\. If DataSync encounters hard links in these situations, the task completes with an error\. To learn more, check your CloudWatch logs\.  
**When copying to HDFS**, hard links aren't supported\. When copying to HDFS, hard links on the source are skipped and logged to CloudWatch\.

**Symbolic links**  
**When copying between an NFS server, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP \(using NFS\), and Amazon EFS**, symbolic links are preserved\.  
**When copying to Amazon S3**, the link target path is stored in the Amazon S3 object\. The link is correctly restored upon transfer to an NFS server, FSx for Lustre, FSx for OpenZFS, FSx for ONTAP, or Amazon EFS\.  
**When copying between an SMB file share, FSx for Windows File Server, and FSx for ONTAP \(using NFS\)**, symbolic links aren't supported\. If DataSync encounters symbolic links in these situations, the task completes with an error\. To learn more, check your CloudWatch logs\.  
**When copying to HDFS**, symbolic links aren't supported\. When copying to HDFS, symbolic links are skipped and logged to CloudWatch\.

**Directories**  
When copying to or from Amazon S3 buckets, directories are represented as empty objects ending with `/`\.

For information on logging with DataSync, see [Monitoring AWS DataSync activity with Amazon CloudWatch](monitor-datasync.md)\.