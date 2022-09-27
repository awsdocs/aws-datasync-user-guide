# Creating an Amazon FSx for NetApp ONTAP location<a name="create-ontap-location"></a>

An AWS DataSync *location* is an endpoint for an Amazon FSx for NetApp ONTAP file system\. You can use the location as a source or destination when copying data\.

## Accessing FSx for ONTAP file systems<a name="create-ontap-location-access"></a>

To access an FSx for ONTAP file system, DataSync mounts a storage virtual machine \(SVM\) on your file system using [network interfaces](datasync-network.md#required-network-interfaces) in your virtual private cloud \(VPC\)\. DataSync creates these network interfaces in your file system’s preferred subnet only when you create a task that includes your FSx for ONTAP location\.

### Supported protocols<a name="create-ontap-location-supported-protocols"></a>

DataSync can connect to an FSx for ONTAP file system's SVM and copy data using the following protocols:
+ **Network File System \(NFS\)** – With the NFS protocol, DataSync uses the `AUTH_SYS` security mechanism with a user ID \(UID\) and group ID \(GID\) of `0` to authenticate with your SVM\.
**Note**  
DataSync currently only supports NFS version 3 with FSx for ONTAP locations\. If you need to copy NFS version 4 access control lists \(ACLs\), [work with an AWS storage specialist](https://iq.aws.amazon.com/services/aws/datasync)\.
+ **Server Message Block \(SMB\)** – With the SMB protocol, DataSync uses credentials you provide to authenticate with your SVM\. When creating your location, you can specify a local user in your SVM or domain user in your Microsoft Active Directory\.

  To copy between FSx for ONTAP file systems using SMB \(or other types of file systems using SMB\), your source and destination locations must belong to the same Active Directory domain or have an Active Directory trust relationship between their domains\.

**Note**  
DataSync can't access FSx for ONTAP file systems using the iSCSI \(Internet Small Computer Systems Interface\) protocol\. 

### Choosing the right protocol<a name="create-ontap-location-choosing-protocol"></a>

To preserve file metadata in FSx for ONTAP migrations, configure your DataSync source and destination locations to use the same protocol\. Between the supported protocols, SMB preserves metadata with the highest fidelity \(see [How DataSync handles metadata and special files](special-files.md) for details\)\.

When migrating from a Unix \(Linux\) server or network\-attached storage \(NAS\) share that serves users through NFS, do the following:

1. [Create an NFS location](create-nfs-location.md) for the Unix \(Linux\) server or NAS share\. \(This will be your source location\.\)

1. Configure the FSx for ONTAP volume you’re transferring data to with the [Unix security style](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/managing-volumes.html#volume-security-style)\.

1. Create a location for your FSx for ONTAP file system that’s configured for NFS\. \(This will be your destination location\.\)

When migrating from a Windows server or NAS share that serves users through SMB, do the following:

1. [Create an SMB location](create-smb-location.md) for the Windows server or NAS share\. \(This will be your source location\.\)

1. Configure the FSx for ONTAP volume you’re transferring data to with the [NTFS security style](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/managing-volumes.html#volume-security-style)\.

1. Create a location for your FSx for ONTAP file system that’s configured for SMB\. \(This will be your destination location\.\)

If your FSx for ONTAP environment uses multiple protocols, we recommend working with an AWS storage specialist\. To learn about best practices for multiprotocol access, see [Enabling multiprotocol workloads with Amazon FSx for NetApp ONTAP](http://aws.amazon.com/blogs/storage/enabling-multiprotocol-workloads-with-amazon-fsx-for-netapp-ontap/)\.

## Creating the location<a name="create-ontap-location-how-to"></a>

To create the location, you need an existing FSx for ONTAP file system\. If you don't have one, see [Getting started with Amazon FSx for NetApp ONTAP](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/getting-started.html) in the *Amazon FSx for NetApp ONTAP User Guide*\.

**To specify an FSx for ONTAP file system**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**, and then choose **Create location**\.

1. For **Location type**, choose **Amazon FSx**\.

   You configure this location as a source or destination later\.

1. For **FSx file system**, choose the FSx for ONTAP file system that you want to use as a location\.

1. For **Storage virtual machine**, choose a storage virtual machine \(SVM\) in your file system where you want to copy data to or from\.

1. For **Mount path**, enter the junction path \(also known as a mount point\) in the SVM volume that you want DataSync to use for copying data \(for example, `/vol1`\)\.
**Tip**  
Don't specify a junction path in the SVM's root volume\. For more information, see [Managing FSx for ONTAP storage virtual machines](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/managing-svms.html) in the *Amazon FSx for NetApp ONTAP User Guide*\.

1. For **Security groups**, choose up to five Amazon EC2 security groups that provide access to your file system's preferred subnet\.

   The security groups must allow outbound traffic on the following ports \(depending on the protocol you use\):
   + **NFS** – TCP ports 111, 635, and 2049 
   + **SMB** – TCP port 445

   Your file system's security groups must also allow inbound traffic on the same ports\. 

1. For **Protocol**, choose the data transfer protocol that DataSync uses to access your file system's SVM\.

   For more information, see [Choosing the right protocol](#create-ontap-location-choosing-protocol)\.

------
#### [ NFS ]

   DataSync uses NFS version 3\.

------
#### [ SMB ]

   Configure a user name, password, and Active Directory domain name \(if needed\) to access the SVM\.
   + For **User**, enter a user name that can mount the location and access the files, folders, and metadata that you need in the SVM\.

     If you provide a user in your Active Directory, note the following:
     + If you're using AWS Directory Service for Microsoft Active Directory, the user must be a member of the **AWS Delegated FSx Administrators** group\.
     + If you're using a self\-managed Active Directory, the user must be a member of either the **Domain Admins** group or a custom group that you specified for file system administration when you created your file system\.

     Make sure that the user has the permissions it needs to copy the data you want:
     + `SE_TCB_NAME` – Required to set object ownership and file metadata\. With this privilege, you also can copy NTFS discretionary access lists \(DACLs\)\.
     + `SE_SECURITY_NAME` – May be needed to copy NTFS system access control lists \(SACLs\)\. This operation specifically requires the Windows privilege, which is granted to members of the **Domain Admins** group\. If you configure your task to copy SACLs, make sure that the user has the required privileges\. For information about copying SACLs, see [Ownership and permissions\-related options](create-task.md#configure-ownership-and-permissions)\.
   + For **Password**, enter the password of the user that you specified who can access the SVM\.
   + \(Optional\) For **Active Directory domain name**, enter the fully qualified domain name \(FQDN\) of the Active Directory that your SVM belongs to\.

     

------

1. \(Optional\) Enter values for the **Key** and **Value** fields to tag the FSx for ONTAP file system\.

   Tags help you manage, filter, and search for your AWS resources\. We recommend creating at least a name tag for your location\. 

1. Choose **Create location**\.