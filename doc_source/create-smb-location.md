# Creating an SMB location<a name="create-smb-location"></a>

A *location* is an endpoint for a Server Message Block \(SMB\) file share, which can be hosted on\-premises or by another cloud provider \(for example, Azure Files\)\.

## Creating the location<a name="create-smb-location-how-to"></a>

Your SMB file share can be a source or destination location for AWS DataSync\.

**To create an SMB location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**\.

1. On the **Locations** page, choose **Create location**\.

1. For **Location type**, choose **Server Message Block \(SMB\)**\.

   You configure this location as a source or destination later\.

1. For **Agents**, choose the agent that you want to connect to your SMB server\.

1. For **SMB Server**, provide the Domain Name System \(DNS\) name or IP address of the SMB server\. 

1. For **Share name**, enter the name of the share exported by your SMB server\.

   You can include a folder from within this share\. Specify the share by using slashes \(for example, `/path/to/folder`\)\.

1. \(Optional\) Expand **Additional settings** and choose a specific **SMB Version** to use\.

   You can also let DataSync automatically choose a version based on negotiation with the SMB server\.

1. For **User**, enter the user who can mount the location and has the permissions to access the SMB server\.

   For more information, see [User](#SMBuser) to understand how to choose a user with sufficient permissions to files, folders, and metadata\.

1. For **Password**, enter the password of the user who can mount the location and has the permissions to access the SMB server\. 

1. \(Optional\) For **Domain**, enter the domain that the SMB server belongs to\.

1. \(Optional\) Select **Add tag** to create tags for your SMB location\.

   A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. 

1. Choose **Create location**\.

## Understanding the location settings<a name="configuring-smb"></a>

**Agent**  
An *agent* is a VM that is deployed in your on\-premises environment to connect to your self\-managed location\. An agent makes it easier to securely transfer data between the self\-managed location and AWS\. You can use an agent for more than one location\.

If a task is using multiple agents, all the agents must have the status **Available** for the task to run\. If you use multiple agents for a source location, the status of all the agents must be **Available** for the task to run\. Agents are automatically updated by AWS on a regular basis, using a mechanism that doesn't interrupt your tasks\. 

**SMB server**  
The name of the SMB server, the IP address, or DNS name of the SMB server\. An agent that is installed on\-premises uses this name to mount the SMB server in a network\. 

**Share name**  
The name of the share exported by your SMB server\. You can include a folder from within this share\. Specify the share by using slashes \(for example `/path/to/folder`\)\.

**SMB version**  
DataSync supports SMB 2\.1 and SMB 3 for mounting an SMB file share\. DataSync can automatically choose a version based on negotiation with the SMB server\.

**User**  
The name of a user who can mount the location and has the permissions to access the SMB file share\. This user can be a local user on your Windows file server or a domain user that's defined in your Microsoft Active Directory\.

To set object ownership, DataSync requires the `SE_RESTORE_NAME` privilege, which is usually granted to members of the built\-in Active Directory groups **Backup Operators** and **Domain Admins**\. Providing a user to DataSync with this privilege also helps ensure sufficient permissions to files, folders, and file metadata, except for NTFS system access control lists \(SACLs\)\.

Additional privileges are required to copy SACLs\. Specifically, this requires the Windows `SE_SECURITY_NAME` privilege, which is granted to members of the **Domain Admins** group\. If you configure your task to copy SACLs, make sure that the user has the required privileges\. To learn more about configuring a task to copy SACLs, see [Ownership and permissions\-related options](create-task.md#configure-ownership-and-permissions)\.

When you copy data between SMB shares and FSx for Windows File Server locations or between two FSx for Windows File Server locations, your source and destination locations must either:
+ Belong to the same Active Directory domain\.
+ Have an Active Directory trust relationship between their domains\.

**Password**  
The password of the user who can mount the location and has the permissions to access files and folders in the SMB file share\. 

**Domain**  
The name of the domain that the user is part of\.

**Tag**  
A *tag* is a key\-value pair that helps you manage, filter, and search for your location\. Adding a tag is optional\. We recommend using tags for naming your resources\. 