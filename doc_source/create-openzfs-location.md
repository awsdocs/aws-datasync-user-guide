# Creating an Amazon FSx for OpenZFS location<a name="create-openzfs-location"></a>

A location is an endpoint for your Amazon FSx for OpenZFS file system\. AWS DataSync uses the location to access your file system by using the network protocol that you specify\.

DataSync mounts your FSx for OpenZFS file system by using elastic network interfaces from the virtual private cloud \(VPC\) that's associated with your file system\. DataSync manages the creation, use, and deletion of these network interfaces for you\. 

## Creating the location<a name="create-openzfs-location-console"></a>

To create the location, you need an existing FSx for OpenZFS file system\. If you don't have one, see [Getting started with Amazon FSx for OpenZFS](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/getting-started.html) in the *Amazon FSx for OpenZFS User Guide*\.

**To create an FSx for OpenZFS location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**, and then choose **Create location**\.

1. For **Location type**, choose **Amazon FSx**\.

   You configure this location as a source or destination later\.

1. For **FSx file system**, choose the FSx for OpenZFS file system that you want to use as a location\. 

1. For **Mount path**, enter the mount path for your FSx for OpenZFS file system\. 

   The path must begin with `/fsx` and can be any existing directory path in the file system\. When the location is used as a source, DataSync reads data from the mount path\. When the location is used as a destination, DataSync writes all data to the mount path\. If a subdirectory isn't provided, DataSync uses the root volume directory \(for example, `/fsx`\)\.

1. For **Security groups**, choose up to five security groups that provide network access to your FSx for OpenZFS file system\. 

   The security groups must provide access to the network ports that are used by the FSx for OpenZFS file system\. The file system must allow network access from the security groups\.

   For more information about security groups, see [File system access control with Amazon VPC](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/limit-access-security-groups.html) in the *Amazon FSx for OpenZFS User Guide*\.

1. \(Optional\) Expand **Additional settings** and for **NFS version** choose the NFS version that DataSync uses to access your file system\.

   By default, DataSync uses NFS version 4\.1\.

1. \(Optional\) Enter values for the **Key** and **Value** fields to tag the FSx for OpenZFS file system\.

   Tags help you manage, filter, and search for your location\. We recommend creating at least a name tag for your location\. 

1. Choose **Create location**\.

## Configuring file system authorization<a name="configure-openzfs-authorization"></a>

DataSync accesses your FSx for OpenZFS file system as an NFS client, mounting the file system as a root user with a user ID \(UID\) and group ID \(GID\) of `0`\.

For DataSync to copy all of your file metadata, you must configure the NFS export settings on your file system volumes using `no_root_squash`\. However, you can limit this level of access to only a specific DataSync task\.

For more information, see [Volume properties](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/managing-volumes.html#volume-properties) in the *Amazon FSx for OpenZFS User Guide*\.

### Configuring NFS exports specific to DataSync \(recommended\)<a name="configure-nfs-export-recommended"></a>

You can configure an NFS export specific to each volume that’s accessed only by your DataSync task\. Do this for the most recent ancestor volume of the mount path that you specify when creating your FSx for OpenZFS location\.

**To configure an NFS export specific to DataSync**

1. Create your [DataSync task](working-with-tasks.md)\.

   This creates the task’s elastic network interfaces that you’ll specify in your NFS export settings\.

1. Locate the private IP addresses of the task's network interfaces by using the Amazon EC2 console or AWS CLI\.

1. For your FSx for OpenZFS file system volume, configure the following NFS export settings for each of the task’s network interfaces:
   + **Client address**: Enter the network interface’s private IP address \(for example, `10.24.34.0`\)\.
   + **NFS options**: Enter `rw,no_root_squash`\.

### Configuring NFS exports for all clients<a name="configure-nfs-export-general"></a>

You can specify an NFS export that allows root access to all clients\.

**To configure an NFS export for all clients**
+ For your FSx for OpenZFS file system volume, configure the following NFS export settings:
  + **Client address**: Enter `*`\.
  + **NFS options**: Enter `rw,no_root_squash`\.