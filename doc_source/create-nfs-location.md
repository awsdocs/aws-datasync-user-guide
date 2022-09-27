# Creating an NFS location<a name="create-nfs-location"></a>

AWS DataSync supports the Network File System \(NFS\) v3, NFS v4\.0, and NFS v4\.1 protocols\. 

**To create an NFS location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**\. The locations that you previously created appear in the list of locations\.

1. On the **Locations** page, choose **Create location**\.

1. For **Location type**, choose **NFS**\. You configure this location as a source or destination later\.

1. For **Agents**, choose the agent that you want to use\. If you have previously created agents, the agents appear in the list\. The agent connects to your self\-managed NFS server and makes it easier to securely transfer data between the self\-managed location and AWS\.

1. For **NFS Server**, provide the Domain Name System \(DNS\) name or IP address of the NFS server\.

1. For **Mount path**, enter the mount path for your NFS location\.

1. \(Optional\) Expand **Additional settings** and choose a specific **NFS Version** to use\.

   By default, DataSync uses NFS version 4\.1\.

1. \(Optional\) Select **Add tag** to create tags for your NFS location\. A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. 

1. When you're done, choose **Create location**\.

For detailed information about these NFS location settings, see [NFS location settings](#configuring-nfs)\.

## NFS location settings<a name="configuring-nfs"></a>

Following, you can find descriptions for the configuration settings for NFS locations in DataSync\.

**Agent**  
An *agent* is a VM that's deployed in your self\-managed environment to connect to your self\-managed location\. An agent makes it easier to securely transfer data between the self\-managed location and AWS\. You can use an agent for more than one location\.

If a task is using multiple agents, all the agents must have the status **Available** for the task to run\. If you use multiple agents for a source location, the status of all the agents must be **Available** for the task to run\. Agents are automatically updated by AWS on a regular basis, using a mechanism that doesn't interrupt your tasks\. 

**NFS server**  
The name of the NFS server, the IP address, or DNS name of the NFS server\. An agent that's installed on\-premises uses this name to mount the NFS server in a network\. 

**Mount path**  
The mount path for your NFS file system\. This path must be a path that's exported by the NFS server, or a subdirectory of an exported path\. This path should be such that it can be mounted by other NFS clients in your network\. For information about how to resolve mount path issues, see [My task status is unavailable and indicates a mount error](troubleshooting-datasync.md#onpremise-location-stuck-mounting)\. 

To transfer all the data in the folder that you specified, DataSync must have permissions to read all the data\. To ensure this, either configure the NFS export with `no_root_squash`, or ensure that the permissions of the files that you want DataSync to transfer allow read access for all users\. Doing either enables the agent to read the files\. For the agent to access directories, you must additionally enable all execute access\.

**Tag**  
A *tag* is a key\-value pair that helps you manage, filter, and search for your location\. Adding a tag is optional\. We recommend using tags for naming your resources\. 

**Note**  
DataSync supports the NFS v3, NFS v4\.0, and NFS v4\.1 protocols\. DataSync automatically chooses the NFS version that it uses when reading from an NFS location\. If you need to force DataSync to use a specific NFS version, see [How do I configure DataSync to use a specific NFS or SMB version to mount my share?](troubleshooting-datasync.md#force-nfs-version)\. 

## NFS server on AWS Snowcone<a name="nfs-on-snowcone"></a>

If you are copying data to or from your AWS Snowcone device, note the following configuration\. 
+ **Agents**: Select the Amazon EC2 agent that you launched on your AWS Snowcone device\. For more information about using DataSync with Snowcone, see [ Using DataSync to transfer files to AWS](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/use-data-sync.html) in the *AWS Snowcone User Guide*\.
+ **NFS server**: Specify the virtual IP address that you attached to the NFS server on your Snowcone device using the AWS OpsHub for Snow Family\. For more information about using AWS OpsHub, see [ Using AWS OpsHub for Snow Family to manage devices](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/aws-opshub.html)\.
+ **Mount path**: Specify the NFS export path for the bucket that you want to transfer data to or from\. The format of the export path of an Amazon S3 bucket is `/buckets/bucket-name`\. For more information about using the AWS Snowcone NFS server, see [Using NFS file shares to manage file storage](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/manage-nfs.html) in the *AWS Snowcone User Guide*\.