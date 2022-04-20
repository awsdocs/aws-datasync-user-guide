# How DataSync handles metadata and special files<a name="special-files"></a>

AWS DataSync saves metadata and special files \(links and directories\) when copying data to and from storage systems and services\.

However, DataSync does not copy system\-level settings\. For example, when copying objects, DataSync doesn't copy your storage system's encryption setting\. If you're copying from an SMB share, DataSync doesn't copy the permissions you configured at the file system level\.

**Topics**
+ [Metadata copied by DataSync](#metadata-copied)
+ [Default POSIX metadata applied by DataSync](#POSIX-metadata)
+ [Links and directories copied by DataSync](#special-files-copied)

## Metadata copied by DataSync<a name="metadata-copied"></a>

DataSync preserves metadata between storage systems that have similar metadata structures\.

**When copying between self\-managed Network File System \(NFS\), Amazon FSx for Lustre, Amazon FSx for OpenZFS, or Amazon EFS, and Amazon EFS, Amazon FSx for Lustre, or Amazon FSx for OpenZFS** – In this case, DataSync can copy the following metadata:
+ File and folder modification timestamps
+ User ID \(UID\) and group ID \(GID\)
+ POSIX permissions

**When copying between Hadoop Distributed File System \(HDFS\) and Amazon EFS, FSx for Lustre, or FSx for OpenZFS** – In this case, DataSync can copy the following metadata:
+ File and folder modification timestamps
+ POSIX permissions

**Note**  
HDFS uses strings to store file and folder user and group ownership, rather than numeric identifiers \(such as UIDs and GIDs\)\. When copying from HDFS to Amazon EFS, FSx for Lustre, or FSx for OpenZFS, default values for UIDs and GIDs are applied on the destination file system\. For more information about default values, see [Default POSIX metadata applied by DataSync](#POSIX-metadata)\.

**When copying between self\-managed Server Message Block \(SMB\) or Amazon FSx for Windows File Server, and FSx for Windows File Server** – In this case, DataSync can copy the following metadata:
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

**When copying between self\-managed NFS, FSx for Lustre, FSx for OpenZFS, or Amazon EFS and Amazon S3** – In this case, the following metadata is stored as Amazon S3 user metadata:
+ File and folder modification timestamps
+ User ID and group ID
+ POSIX permissions

The file metadata that is stored in Amazon S3 user metadata is interoperable with NFS shares on file gateways in AWS Storage Gateway\. A file gateway enables low\-latency access from on\-premises networks to data that was copied to Amazon S3 by DataSync\. This metadata is also interoperable with Amazon FSx for Lustre\.

When DataSync copies objects that contain this metadata back to an NFS server, the file metadata is restored\. Restoring metadata requires granting elevated permissions to the NFS server\. For more information, see [Creating a location for NFS](create-nfs-location.md)\.

**When copying between HDFS and Amazon S3** – In this case, the following metadata is stored as Amazon S3 user metadata:
+ File and folder modification timestamps
+ User name and group name
+ POSIX permissions

**Note**  
HDFS uses strings to store file and folder user and group ownership, rather than numeric identifiers, such as UIDs and GIDs\. DataSync ignores user and group name metadata values stored in Amazon S3 when copying to EFS or self\-managed NFS\.

**When copying between self\-managed object storage and Amazon S3 or between two Amazon S3 buckets** – In this case, DataSync only copies user\-defined metadata and tags\. 

**Note**  
DataSync doesn't copy other object information, such as object access control lists \(ACLs\) or prior object versions\.

**When copying between storage systems that don't have similar metadata structure** – In this case, DataSync sets metadata using the following rules\.


| If you copy this way | This happens to metadata | 
| --- | --- | 
|  From an SMB share to Amazon EFS, FSx for Lustre, FSx for OpenZFS, or Amazon S3  From FSx for Windows File Server to an NFS share or HDFS  |  Default POSIX metadata is set for all files and folders on the target NFS server, FSx for Lustre file system, FSx for OpenZFS file system, or Amazon EFS file system, or stored in the Amazon S3 object's metadata\. This approach includes using the default POSIX user ID and group ID values\. On HDFS, file and folder timestamps are applied from the source\. The file or folder owner is set based on the user or Kerberos principal specified in DataSync\. The Groups Mapping configuration on the Hadoop cluster determines the group\.  | 
|  From an NFS share or HDFS to FSx for Windows File Server  From Amazon EFS, FSx for Lustre, FSx for OpenZFS, or Amazon S3 to an SMB share  |  File and folder timestamps are applied from the source\. Ownership is set based on the Windows user that was specified in DataSync to access the Amazon FSx or SMB share\. Permissions are inherited from the parent directory\.  | 

## Default POSIX metadata applied by DataSync<a name="POSIX-metadata"></a>

When the source and destination don't have a similar metadata structure, or when source metadata is missing, DataSync applies default POSIX metadata\.

Specifically, DataSync applies this metadata in these situations:
+ When transferring files from an Amazon S3 or self\-managed object storage location to an Amazon EFS, FSx for Lustre, FSx for OpenZFS, NFS, or HDFS location, in cases where Amazon S3 objects don't have DataSync POSIX metadata
+ When transferring from an SMB location to an NFS, HDFS, Amazon S3, FSx for Lustre, FSx for OpenZFS, or Amazon EFS location

The following table shows the default POSIX metadata and permissions that DataSync applies\.


| Permission | Value | 
| --- | --- | 
|  UID  |  65534  | 
|  GID  |  65534  | 
|  Folder Permission  |  0755  | 
|  File Permission  |  0644  | 

HDFS stores file and folder user and group ownership using strings, rather than numeric identifiers, such as UIDs and GIDs\. When there is no equivalent metadata on the source location, file and folder ownership is set based on the user or Kerberos principal that you specified in DataSync\. The group is determined by the Groups Mapping configuration on the Hadoop cluster\. 

## Links and directories copied by DataSync<a name="special-files-copied"></a>

Understand how DataSync handles copied hard links, symbolic links, and directories in different storage locations\.

**Hard links**  
**When copying between an NFS server, FSx for Lustre, FSx for OpenZFS, and Amazon EFS**, hard links are preserved\.  
**When copying to Amazon S3**, each hard link is transferred only once\. Separate Amazon S3 objects are created for each copy\. If a hard link is unchanged in Amazon S3, it's correctly restored upon transfer to an NFS server, FSx for Lustre, FSx for OpenZFS, or Amazon EFS\.  
**When copying between SMB file shares and FSx for Windows File Server**, hard links aren't supported\. If DataSync encounters hard links in such a copy, they're skipped and logged to Amazon CloudWatch Logs\. For more information about how DataSync works with CloudWatch Logs, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\.   
**When copying to HDFS**, hard links aren't supported\. When copying to HDFS, hard links on the source are skipped and logged to Amazon CloudWatch Logs\. 

**Symbolic links**  
**When copying between an NFS server, FSx for Lustre, FSx for OpenZFS, and Amazon EFS**, symbolic links are preserved\.  
**When copying to Amazon S3**, the link target path is stored in the Amazon S3 object\. The link is correctly restored upon transfer to an NFS server, FSx for Lustre, FSx for OpenZFS, or Amazon EFS\.  
**When copying between SMB file shares and FSx for Windows File Server**, symbolic links aren't supported\. If DataSync encounters symbolic links in such a copy, they're skipped and logged to CloudWatch Logs\. For more information about how DataSync works with CloudWatch Logs, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\.  
**When copying to HDFS**, symbolic links aren't supported\. When copying to HDFS, symbolic links are skipped and logged to Amazon CloudWatch Logs\. 

**Directories**  
When copying to or from Amazon S3 buckets, directories are represented as empty objects ending with `/`\.