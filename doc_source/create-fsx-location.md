# Creating a location for FSx for Windows File Server<a name="create-fsx-location"></a>

A location is an endpoint for your Amazon FSx for Windows File Server\. AWS DataSync accesses your FSx for Windows File Server using the Server Message Block \(SMB\) protocol\. 

DataSync authenticates against your FSx for Windows File Server file system with a user name and password that you configure in the DataSync console or AWS CLI\. When you copy data between SMB shares and Amazon FSx or between Amazon FSx locations, the source and destination must belong to the same Active Directory domain or have an Active Directory trust relationship between their domains\.

See [User](#FSxWuser) to learn more about choosing a user that ensures sufficient permissions to files, folders, and metadata\. 

The DataSync service mounts your file system from your virtual private cloud \(VPC\) using elastic network interfaces managed by the DataSync service\. DataSync fully manages the creation, the use, and the deletion of these network interfaces on your behalf\. 

If you don't have an FSx for Windows File Server in the current AWS Region, create one\. For information about how to create an FSx for Windows File Server, see [Getting started with Amazon FSx ](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/getting-started.html) in the *Amazon FSx for Windows File Server User Guide*\.

**Note**  
DataSync currently doesn't support transferring files to FSx for Windows File Server volumes that are in dedicated tenancy VPCs\. For information about dedicated tenancy VPCs, see [Creating a VPC with an instance tenancy of dedicated](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html#creatingdedicatedvpc) in the *Amazon EC2 User Guide for Linux Instances*\. 

**To create an Amazon FSx location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Locations**\. The locations that you previously created appear in the list of locations\.

1. Choose **Create Location** to open the **Create location** page\. For **Location type**, choose **Amazon FSx for Windows File Server**\.

1. For **FSx for Windows File system**, choose the FSx for Windows File Server that you want to use as an endpoint\. You configure this location as a source or destination later\.

1. For **Share name**, enter the mount path for your Amazon FSx file server\. The path can include a subdirectory\. If so, this is a subdirectory in the FSx for Windows File Server that's used to read data from the FSx location or write data to the Amazon FSx destination\.
**Note**  
The subdirectory must be specified with forward slashes \(for example, `//FSx.DNS/share/path/to/folder`\)\.

1. For **Security Group**, the DataSync console automatically chooses the default security group of the subnet for the chosen FSx for Windows File Server\. We recommend using these default settings\. 
**Note**  
DataSync uses the security group specified in this step to connect to your FSx for Windows File Server\. If the security group is configured to disallow connections from within itself, you have two options:  
Change the security group configuration to allow the security group to communicate within itself\.
Choose a different security group, so the selected security group can communicate with the mount target's security group\.

1. In the **User settings** section, provide the information for FSx for Windows File Server:

**User**  
The user that can mount the location and has the permissions to access the Amazon FSx server\. 

   To ensure sufficient permissions to files, folders, and file metadata, we recommend that you make this user a member of the file system administrators group\. If you are using AWS Directory Service for Microsoft Active Directory with FSx for Windows File Server, the user must be a member of the **AWS Delegated FSx Administrators** group\. If you are using a self\-managed Microsoft Active Directory with your FSx for Windows File Server, the user must be a member of one of two groups\. These are the group of **Domain Admins** or the custom group you specified for file system administration when you created your file system\.

   To set object ownership, DataSync requires the `SE_RESTORE_NAME` privilege, which is usually granted to members of the built\-in Active Directory groups **Backup Operators** and **Domain Admins**\. Providing a user to DataSync with this privilege also helps ensure sufficient permissions to files, folders, and file metadata *except for NTFS system access control lists \(SACLs\)*\. 

   Additional privileges are required to copy SACLs\. Specifically, this requires the Windows `SE_SECURITY_NAME` privilege, which is granted to members of the **Domain Admins** group\. If your task will be configured to copy SACLs, make sure that the user has the required privileges\. To learn more about configuring a task to copy SACLs, see [Ownership and permissions\-related options](create-task.md#configure-ownership-and-permissions)\. 

   When you copy data between SMB shares and Amazon FSx, or between two Amazon FSx locations, both the source and the destination must belong to the same Active Directory domain, or have an Active Directory trust relationship between their domains\.

**Password**  
The password of the user that can mount the location and has the permissions to access files and folders in the FSx for Windows File Server\. 

**Domain**  
\(Optional\) The name of the domain the FSx for Windows File Server belongs to\.

1. \(Optional\) Provide values for the **Key** and **Value** fields to tag the FSx for Windows File Server\. A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. We recommend using tags to name your resources\. 

1. When you are done, choose **Create location**\. The location that you just created appears in the list of locations\.