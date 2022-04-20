# Creating your DataSync task<a name="creating-task"></a>

If this is your first time using DataSync, the instructions in [Getting started with AWS DataSync](getting-started.md) walk you through the process of creating a task\. 

**Topics**
+ [Prerequisite: Creating the locations for your DataSync task](#creating-tasks-endpoints)
+ [Creating a task to transfer data between self\-managed storage and AWS](#Task-onpremises-aws)
+ [Creating a task to transfer between in\-cloud locations](#in-coud-setup)
+ [Configuring task settings](#configuring-task)

## Prerequisite: Creating the locations for your DataSync task<a name="creating-tasks-endpoints"></a>

A DataSync task requires a source and destination location to transfer data between\.
+ [Creating a location for NFS](create-nfs-location.md)
+ [Creating a location for SMB](create-smb-location.md)
+ [Creating a location for HDFS](create-hdfs-location.md)
+ [Creating a location for object storage](create-object-location.md)
+ [Creating a location for Amazon EFS](create-efs-location.md)
+ [Creating a location for FSx for Windows File Server](create-fsx-location.md)
+ [Creating a location for FSx for Lustre](create-lustre-location.md)
+ [Creating a location for FSx for OpenZFS](create-openzfs-location.md)
+ [Creating a location for Amazon S3](create-s3-location.md)

For a list of supported DataSync locations and transfer scenarios, see [Working with locations](working-with-locations.md)\.

## Creating a task to transfer data between self\-managed storage and AWS<a name="Task-onpremises-aws"></a>

If you have previously created a task and want to create additional tasks, use the following procedure\.

**To create a task**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Tasks**, and then choose **Create task**\.

1. On the **Configure source location** page, choose** Create new location** and configure a new location if you want to use a new location for your source\. Provide the configuration settings and choose **Next**\. For instructions on how to create a location, see [Working with locations](working-with-locations.md)\.

   If you want to use a source location that you previously created, choose **Choose existing location**, choose your source location from the list, and then choose **Next**\.

   For step\-by\-step instruction, see [Configure a source location](configure-source-location.md)\.

## Creating a task to transfer between in\-cloud locations<a name="in-coud-setup"></a>

Use the following instructions to set up the DataSync agent on an Amazon EC2 instance for data transfers\. The examples in this section cover these use cases: 
+ [Data transfer from in\-cloud file system to in\-cloud file system or Amazon S3](using-ec2-agent-in-region.md#efs-efs) – Transfer data from Amazon EFS to Amazon EFS, from self\-managed NFS to EFS, or to Amazon S3\.
+ [Data transfer from S3 to in\-cloud file systems](using-ec2-agent-in-region.md#s3-cloud-nfs) – Transfer data from Amazon S3 to Amazon EFS, or from Amazon S3 to self\-managed NFS\.

### Creating a task to transfer from in\-cloud NFS to in\-cloud NFS or Amazon S3<a name="task-efs-efs"></a>

Use the following instructions to transfer data from an in\-cloud NFS file system to AWS\. To perform this transfer, the DataSync agent must be located in the same AWS Region and same AWS account where the file system is deployed\. This type of transfer includes transfers from EFS to EFS, transfers from self\-managed NFS to Amazon EFS, and transfers to Amazon S3\. For information about how in\-cloud NFS to in\-cloud NFS or Amazon S3 works, see [Data transfer from in\-cloud file system to in\-cloud file system or Amazon S3](using-ec2-agent-in-region.md#efs-efs)\.

**Note**  
Deploy the agent in the AWS Region and AWS account where the source EFS or self\-managed NFS file system resides\.

#### Deploying your DataSync agent as an Amazon EC2 instance to read files from in\-cloud<a name="task-deploy-ec2-agent"></a><a name="task-efs-efs-steps"></a>

**To deploy the DataSync agent as an Amazon EC2 instance**

1. From the AWS account where the source EFS resides, launch the agent by using your Amazon Machine Image \(AMI\) from the Amazon EC2 launch wizard\. Use the following URL to launch the AMI\.

   ```
   https://console.aws.amazon.com/ec2/v2/home?region=source-efs-or-nfs-region#LaunchInstanceWizard:ami=ami-id
   ```

   In the URL, replace the `source-efs-or-nfs-region` and *`ami-id`* with your own\. 

   After the AMI launches, the **Choose an Instance Type** appears on the Amazon EC2 console\. For a list of AMI IDs by AWS Region, see [Deploy your agent as an Amazon EC2 instance](deploy-agents.md#ec2-deploy-agent)\.

1. Choose one of the recommended instance types for your use case, and choose ****Next**: Configure Instance Details**\. For the recommended instance types, see [Amazon EC2 instance requirements](agent-requirements.md#ec2-instance-types)\.

1. On the **Configure Instance Details** page, do the following:

   1. For **Network**, choose the VPC where your source EFS or NFS is located\.

   1. Choose a value for **Auto\-assign Public IP**\. If you want your instance to be accessible from the public internet, set **Auto\-assign Public IP** to **Enable**\. Otherwise, set **Auto\-assign Public IP** to **Disable**\. If a public IP address isn't assigned, activate the agent in your VPC using its private IP address\.

      When you transfer files from an in\-cloud NFS, to increase performance, we recommend that you choose the **Placement Group** where your NFS server resides\.

1. Choose **Next: Add Storage**\. The agent doesn't require additional storage, so you can skip this step and choose** Next: Add tags**\.

1. \(Optional\) On the **Add Tags** page, you can add tags to your Amazon EC2 instance\. When you're finished on the page, choose** Next: Configure Security Group**\.

1. On the **Configure Security Group** page, do the following:

   1. Make sure that the selected security group allows inbound access to HTTP port 80 from the web browser that you plan to use to activate the agent\.

   1. Make sure that the security group of source EFS or NFS allows inbound traffic from the agent\. In addition, make sure that the agent allows outbound traffic to the source EFS or NFS\. The traffic goes through the standard NFS port, 2049\.

   For the complete set of network requirements for DataSync, see [Network requirements](datasync-network.md)\.

1. Choose **Review and Launch** to review your configuration, then choose **Launch** to launch your instance\. Remember to use a key pair that's accessible to you\. A confirmation page appears and indicates that your instance is launching\.

1. Choose **View Instances** to close the confirmation page and return to the Amazon EC2 instances screen\. When you launch an instance, its initial state is **pending**\. After the instance starts, its state changes to **running**\. At this point, it's assigned a public Domain Name System \(DNS\) name and IP address, which can be found in the **Descriptions** tab\.

1. If you set **Auto\-assign Public IP** to **Enable**, choose your instance and note the public IP address in the **Description** tab\. You use this IP address later to connect to your sync agent\. 

   If you set **Auto\-assign Public IP** to **Disable**, launch or use an existing instance in your VPC to activate the agent\. In this case, you use the private IP address of the sync agent to activate the agent from this instance in the VPC\.

#### Creating a task to transfer data from EFS or self\-managed storage<a name="task-efs-incloud-nfs"></a>

Next, you create a task to transfer data\.

**Note**  
 Create the task in the AWS Region and AWS account where the destination EFS or Amazon S3 bucket resides\.

**To create a task**

1. Open the DataSync console in the AWS Region where your destination Amazon EFS file system is located\. The destination EFS or Amazon S3 bucket must be in the same AWS account\.

1. Choose **Create task**, then choose **On\-premises to AWS** on the **Use case options** page, and then choose **Create agent**\.

1. In the **Create agent** wizard's **Activation** section, enter the Amazon EC2 instance's IP address for **Agent address**, and then choose **Get key**\. This IP address can be private or public\. For more details, see step 9 of [To deploy the DataSync agent as an Amazon EC2 instance](#task-efs-efs-steps)\.

   Your browser connects to this IP address to get a unique activation key from your agent\. This key securely associates your agent with your AWS account\. This IP address doesn't need to be accessible from outside your network, but must be accessible from your browser\.

1. Enter an agent name that you can easily identify later, and choose **Create agent** when done\. You can optionally add tags to the agent\.

1. Choose **Tasks** from the navigation pane\. 

1. Choose **On\-premises to AWS**, and choose **Next** to open the **Source configuration** page\.

1. In the **Source location options**, choose **Create new location** and choose **Network File System \(NFS\) or Server Message Block \(SMB\)**\. Fill in the following options:
   + For agent, choose your newly created agent from the list\. 
   + If you are copying from EFS, do the following: 
     + For **NFS Server**, enter the **DNS name** of your source EFS\. 
     + For **Mount path**, enter **/** \(forward slash\) and choose **Next**\.
   + If you are copying from self\-managed NFS or SMB, do the following: 
     + For **NFS Server**, enter the private DNS or IP address of your source NFS\. 
     + For **Mount path**, enter a path that's exported by your NFS server and choose **Next**\. For more information, see [Creating an NFS location](create-locations-cli.md#create-location-nfs-cli)\. 

1. Choose **Create new location**\. This is the destination location for your data transfer\. Fill in the following options:
   + If you are copying to EFS, do the following: 
     + For **Location type**, choose **EFS**\.
     + Choose your destination EFS\. 
     + For **Mount path**, enter **/** \(forward slash\)\. 
     + For **Subnet** and **Security groups**, use the default settings and choose **Next**\.
   + If you are copying to Amazon S3, do the following: 
     + For **Location type**, choose Amazon S3 bucket\. 
     + For **Amazon S3 bucket**, choose your source Amazon S3 bucket\.
     + For **Folder**, choose a folder prefix to use for the transfer, or you can keep it blank\.
     + Choose your destination Amazon S3 bucket and an optional folder\. DataSync can generate an AWS Identity and Access Management \(IAM\) role to access your bucket, or you can create on your own\.

1.  Choose **Next**, and optionally name the task and add tags\. 

1. Choose or create an Amazon CloudWatch Logs log group at the bottom of the page, and choose **Next**\. For more information on working with CloudWatch Logs, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\.

1. Review the settings on the next page, and choose **Create task**\.

1. Choose **Start** to run the task that you just created to start transferring data\.

### Creating a task to transfer from Amazon S3 to in\-cloud NFS<a name="task-s3-cloud-nfs"></a>

Use the following instructions to transfer data from Amazon S3 to an in\-cloud NFS file system that's located in the same AWS account and AWS Region where the agent is deployed\. This approach includes transfers from Amazon S3 to EFS, or from Amazon S3 to self\-managed NFS\. The following diagram illustrates this type of transfer\. For information about how Amazon S3 to in\-cloud NFS works, see [Data transfer from S3 to in\-cloud file systems](using-ec2-agent-in-region.md#s3-cloud-nfs)\.

#### Deploying the DataSync agent on an Amazon EC2 instance to write to your destination location<a name="task-ec2-deploy-agent-s3"></a>

First, deploy the DataSync agent on an Amazon EC2 instance in the AWS Region and AWS account where the destination EFS file system or self\-managed NFS server resides\. 

**To deploy the agent**
+ Launch the agent from the selected AMI by using the Amazon EC2 launch wizard\. To do so, use the following URL\.

  ```
  https://console.aws.amazon.com/ec2/v2/home?region=DESTINATION-EFS-or-NFS-REGION#LaunchInstanceWizard:ami=AMI-ID. 
  ```

  In the URL, replace the AWS Region and AMI ID with your own\. You are redirected to the **Choose an Instance Type** page on the Amazon EC2 console\. For a list of AMI IDs by AWS Region, see [Deploy your agent as an Amazon EC2 instance](deploy-agents.md#ec2-deploy-agent)\.

#### Creating a task to transfer data from Amazon S3<a name="task-ec2-create-task-s3"></a>

Next, you create a task to transfer data\.

**Note**  
Create the task in the AWS account and AWS Region where the source Amazon S3 bucket resides\.

**To create a task that transfers data from Amazon S3 to EFS or a self\-managed NFS or SMB**

1. Open the DataSync console in the AWS Region where your source Amazon S3 bucket is located\.

1. Choose **Create task**, and choose the use case **AWS to on\-premises**\.

1. Choose **Create agent**\.

1. If you set **Auto\-assign Public IP** to **Enable**, choose your instance and note the public IP address in the **Description** tab\. You use this IP address later to connect to your sync agent\. 

   If you set **Auto\-assign Public IP** to **Disable**, launch or use an existing instance in your VPC to activate the agent\. In this case, you use the private IP address of the sync agent to activate the agent from this instance in the VPC\.

1. In the **Create agent** wizard, for **Agent address** enter the Amazon EC2 instance's IP address \(private or public, as explained in step 3\), and then choose **Get key**\.

   Your browser connects to this IP address to get a unique activation key from your agent\. This key securely associates your agent with your AWS account\. This IP address doesn't need to be accessible from outside your network, but must be accessible from your browser\.

1. Choose an agent name that you can easily identify later\. You can optionally add tags\. When you're done, choose **Create agent**\. 

1. Choose **AWS to on\-premises**, and choose **Next**\. 

1. Choose **Create new location**: 
   + For **Location type**, choose Amazon S3 bucket\. 
   + For **Amazon S3 bucket**, choose your source Amazon S3 bucket\.
   + For **Folder**, choose a folder prefix for the transfer, or you can keep it blank\. 

     DataSync can generate an IAM role to access your bucket, or you can create on your own\.

1. Choose **Next**\. Choose **Create new location**, choose **NFS or SMB** for **Location type**, and choose the agent that you just created from the list\.

1. 

   1. If you are copying to EFS, do the following: 
      + For **NFS Server**, enter the** DNS name** of your source EFS\. 
      + For **Mount path**, enter **/** \(forward slash\) and choose **Next**\.

   1. If you are copying to in\-cloud NFS, do the following:
      + For **NFS Server**, enter the private DNS or IP address of your source NFS\. 
      + For **Mount path**, enter a path that is exported by your NFS server\. For more information, see [Creating an NFS location](create-locations-cli.md#create-location-nfs-cli)\.

1. Choose **Next**, and optionally name the task and add tags\. 

1. Choose or create a CloudWatch Logs log group at the bottom of the page, and choose **Next**\. For more information on working with CloudWatch Logs, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\.

1. Review the settings on the next page, and choose **Create task**\.

1. Choose **Start** to run the task that you just created to transfer data, and then choose **Start** again on the **Start Task** page\.

## Configuring task settings<a name="configuring-task"></a>

Following, you can find information on how to configure a task setting\. You use these settings to control how a task execution behaves\. These settings are available in the **Options** section\.

These options control the behavior of a task execution\. Behavior includes preserving metadata such as the user ID \(UID\) or group ID \(GID\), preserving file permissions, and data integrity verification\. If you don't specify values for these options, DataSync uses a set of default options that can be overridden for a task execution\.

For more information about configuring a DataSync task, see [Configure task settings](create-task.md)\. 

The available options are as follows:
+ **Data verification options** – Task data verification options specify how to verify data that's transferred by the task\. For more information about configuring these options, see [Data verification options](create-task.md#configure-data-verification-options)\. 
+ **Ownership and permissions\-related options** – DataSync preserves metadata between storage systems that have similar metadata structures\. Depending on the storage system type, different options are used to configure such metadata preservation\. For more information about configuring these options, see [Ownership and permissions\-related options](create-task.md#configure-ownership-and-permissions)\. 
+ **File metadata options and file management** – You can configure DataSync tasks to copy file metadata, to keep deleted files, and to overwrite files in the destination\. For more information about configuring file metadata and file management options, see [File metadata options and file management](create-task.md#configure-file)\. 
+ **Bandwidth options** – You can configure a bandwidth limit for DataSync tasks\. For more information about configuring bandwidth options, see [Bandwidth options](create-task.md#configure-bandwidth)\.
+ **Filtering options** – When you transfer data from your source to your destination location, you can apply filters to transfer only a subset of the files in your source location\. For more information about configuring filtering options, see [Filtering options](create-task.md#configure-filter)\.
+ **Scheduling and queueing options** – You can schedule a DataSync task to be run at a specific time\. If you are using a single agent to run multiple tasks, you can queue those tasks\. For more information about configuring scheduling and queueing options, see [Scheduling and queueing options](create-task.md#configure-scheduling-queueing)\. 
+ **Tags and logging options** – You can add one or more tags to a DataSync task\. You can also choose logging options to have DataSync publish logs for individual files or objects to the CloudWatch log group that you specify\. For more information about configuring tags and logging options, see [Tags and logging options](create-task.md#configure-logging)\. 