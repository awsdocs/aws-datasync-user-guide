# Creating a location for FSx for Lustre<a name="create-lustre-location"></a>

A location is an endpoint for your Amazon FSx for Lustre file system\. AWS DataSync uses the information that you provide in the location to access your file system as a Lustre client\. 

The DataSync service mounts your FSx for Lustre file system from your virtual private cloud \(VPC\) using elastic network interfaces managed by the DataSync service\. DataSync manages the creation, use, and deletion of these network interfaces on your behalf\. 

For more information about FSx for Lustre file systems, see [What is Amazon FSx for Lustre?](https://docs.aws.amazon.com/fsx/latest/LustreGuide/what-is.html)

**Authorization**  
DataSync connects to your FSx for Lustre file system using the Lustre client\. DataSync requires access to all data on your FSx for Lustre file system\. To have this level of access, DataSync mounts your file system as the root user using a user ID \(UID\) and group ID \(GID\) of `0`\.

**To create an FSx for Lustre location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Locations**, and then choose **Create location**\.

1. For **Location type**, choose **Amazon FSx**\.

   You configure this location as a source or destination later\. 

1. For **FSx file system**, choose the FSx for Lustre file system that you want to use as a location\. 

1. For **Mount path**, enter the mount path for you FSx for Lustre file system\. The path can include a subdirectory\. When the location is used as a source, DataSync reads data from the mount path\. When the location is used as a destination, DataSync writes all data to the mount path\. If a subdirectory isn't provided, DataSync uses the root directory \(`/`\)\.

1. For **Security groups**, select up to five security groups that provide network access to your FSx for Lustre file system\. The security groups must provide access on the network ports used by the FSx for Lustre file system\. The FSx for Lustre file system must allow network access from the security groups that you select\. 

   For more information about security groups, see [File System Access Control with Amazon VPC](https://docs.aws.amazon.com/fsx/latest/LustreGuide/limit-access-security-groups.html) in the *Amazon FSx for Lustre User Guide*\.

1. \(Optional\) Provide values for the **Key** and **Value** fields to tag the FSx for Lustre file system\. Tags help you manage, filter, and search for your location\. We recommend using tags for naming your resources\. 

1. When you're done, choose **Create location**\. The location that you just created appears in the list of locations\. 