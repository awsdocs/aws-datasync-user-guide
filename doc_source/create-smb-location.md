# Creating a location for SMB<a name="create-smb-location"></a>

When you use a location in a task, you configure it as the source or destination location\. AWS DataSync supports the Server Message Block \(SMB\) 2\.1 and SMB 3 protocols\. DataSync authenticates by using a user name and a password that you provide\. This user can be a local user on your Windows file server, or it can be a domain user defined in your Active Directory\. 

When you copy data between SMB shares and Amazon FSx, both the source and destination must belong to the same Active Directory domain or have an Active Directory trust relationship between their domains\. See [User](#SMBuser) to learn more about choosing a user that ensures sufficient permissions to files, folders, and metadata\. 

**To create an SMB location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Locations**\. The locations that you previously created appear in the list of locations\.

1. On the **Locations** page, choose **Create location**\.

1. For **Location type**, choose **Server Message Block \(SMB\)**\. You configure this location as a source or destination later\.

1. For **Agents**, choose the agent that you want to use\. The agent connects to your self\-managed SMB server and makes it easier to securely transfer data between the self\-managed location and AWS\.

1. For **SMB Server**, provide the Domain Name System \(DNS\) name or IP address of the SMB server\. 

1. For **Share name**, enter the name of the share exported by your SMB server\. You can include a folder from within this share\. Specify the share by using slashes \(for example, `/path/to/folder`\)\.

1. \(Optional\) Expand **Additional settings** and choose a specific **SMB Version** to use\. You can also let DataSync automatically choose a version based on negotiation with the SMB server\.

1. For **User**, enter the user who can mount the location and has the permissions to access the SMB server\. See [User](#SMBuser) to learn more about choosing a user that ensures sufficient permissions to files, folders, and metadata\.

1. For **Password**, enter the password of the user who can mount the location and has the permissions to access the SMB server\. 

1. \(Optional\) For **Domain**, enter the domain that the SMB server belongs to\.

1. \(Optional\) Select **Add tag** to create tags for your SMB location\. A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. 

1. When you're done, choose **Create location**\.

## SMB location settings<a name="configuring-smb"></a>

Following, you can find descriptions for the configuration settings for SMB locations in DataSync\.

**Agent**  
An *agent* is a VM that is deployed in your on\-premises environment to connect to your self\-managed location\. An agent makes it easier to securely transfer data between the self\-managed location and AWS\. You can use an agent for more than one location\.

If a task is using multiple agents, all the agents must have the status **Available** for the task to run\. If you use multiple agents for a source location, the status of all the agents must be **Available** for the task to run\. Agents are automatically updated by AWS on a regular basis, using a mechanism that doesn't interrupt your tasks\. 

**SMB server**  
The name of the SMB server, the IP address, or DNS name of the SMB server\. An agent that is installed on\-premises uses this name to mount the SMB server in a network\. 

**Share name**  
The name of the share exported by your SMB server\. You can include a folder from within this share\. Specify the share by using slashes, for example `/path/to/folder`\.

**User**  
The user that can mount the location and has the permissions to access the SMB file share\. This user can be a local user on your Windows file server, or it can be a domain user defined in your Active Directory\.

 To set object ownership, DataSync requires the `SE_RESTORE_NAME` privilege, which is usually granted to members of the built\-in Active Directory groups **Backup Operators** and **Domain Admins**\. Providing a user to DataSync with this privilege also helps ensure sufficient permissions to files, folders, and file metadata *except for NTFS system access control lists \(SACLs\)*\.

Additional privileges are required to copy SACLs\. Specifically, this requires the Windows `SE_SECURITY_NAME` privilege, which is granted to members of the **Domain Admins** group\. If your task will be configured to copy SACLs, make sure that the user has the required privileges\. To learn more about configuring a task to copy SACLs, see [Ownership and permissions\-related options](create-task.md#configure-ownership-and-permissions)\. 

When you copy data between SMB shares and FSx for Windows File Server locations, or between two FSx for Windows File Server locations, both the source and the destination must belong to the same Active Directory domain, or have an Active Directory trust relationship between their domains\.

**Password**  
The password of the user who can mount the location and has the permissions to access files and folders in the SMB file share\. 

**Domain**  
The name of the domain that the user is part of\.

**SMB version**  
 DataSync automatically chooses the SMB version that it uses to read from an SMB location\. If you need DataSync to use a specific SMB version, use this optional parameter\.

**Tag**  
A *tag* is a key\-value pair that helps you manage, filter, and search for your location\. Adding a tag is optional\. We recommend using tags for naming your resources\. 