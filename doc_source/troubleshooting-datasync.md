# Troubleshooting AWS DataSync issues<a name="troubleshooting-datasync"></a>

Use the following information to troubleshoot AWS DataSync issues\.

## How do I connect to an Amazon EC2 agent's local console?<a name="local-console-ec2"></a>

Make sure the Amazon EC2 instance's security group allows access with SSH \(TCP port 22\), then log in with the following command:

ssh \-i PRIVATE\-KEY admin@AGENT\-PUBLIC\-DNS\-NAME
+ The user name is **admin**\.
+ The `PRIVATE-KEY` value is the `.pem` file containing the private certificate of the Amazon EC2 key pair that you used to launch the instance\. For more information, see [retrieve the public key from the private key](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#retrieving-the-public-key) in the *Amazon EC2 User Guide for Linux Instances\.*
+ The `AGENT-PUBLIC-DNS-NAME` value is the public DNS name of your agent\. You can find this public DNS name by choosing the instance in the Amazon EC2 console and going to the **Description** tab\.

For more information on connecting to the Amazon EC2 instance, see [Connect to your instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html) in the *Amazon EC2 User Guide for Linux Instances\.*

## What does the Failed to retrieve agent activation key error mean?<a name="vpc-activation-error"></a>

When activating your DataSync agent, the agent connects to the endpoint you specify to request an activation key\. You can get this error in non\-VPC endpoint situations\. For example, when your agent is deployed on\-premises and your firewall settings block the connection\. You can also get this error if your agent is deployed as an Amazon EC2 instance and the security groups are locked down\. 

**Action to take**  
Verify that your security group is set up to allow your agent to connect to the VPC endpoint and that you have allowed the required ports\. For information about required ports, see [AWS DataSync network requirements](datasync-network.md)\.

Also, check your firewall and router settings and make sure that they allow communication with endpoints in AWS\. For information about endpoint communication, see [Network requirements for public or FIPS endpoints](datasync-network.md#using-public-endpoints)\.

## I can't activate an agent using a VPC endpoint<a name="vpc-activation-failed"></a>

If you are having issues when you are activating an agent that is created using a VPC endpoint, open a support channel against your VPC endpoint elastic network interface\. For information about Support Channel, see [Getting help with your agent from AWS Support](local-console-vm.md#enable-support-access)\. 

## I don't know what's going on with my agent\. Can someone help me?<a name="enable-support-access2"></a>

If you're having issues with your DataSync agent that you can't solve, see [Getting help with your agent from AWS Support](local-console-vm.md#enable-support-access)\.

## How do I configure DataSync to use a specific NFS or SMB version to mount my share?<a name="force-nfs-version"></a>

For locations that support Network File System \(NFS\) or Server Message Block \(SMB\), DataSync by default chooses the protocol version for you\. You can also specify the version yourself by using the DataSync API, AWS CLI, or AWS Management Console\.

**Action to take \(DataSync API\)**  
Specify the `Version` parameter when creating a location \(for example, see [CreateLocationNfs](API_CreateLocationNfs.md), [CreateLocationSmb](API_CreateLocationSmb.md)\)\. You can also set this parameter for DataSync locations that allow you to update their configuration \(such as NFS and SMB locations\)\.

**Action to take \(AWS CLI\)**  
Similar to the DataSync API, you can specify a location's NFS or SMB version by using the AWS CLI\.

The following example command creates an NFS location that DataSync mounts using NFS version 4\.0\.

```
$ aws datasync create-location-nfs --server-hostname your-server-address \
   --on-prem-config AgentArns=your-agent-arns \
   --subdirectory nfs-export-path \
   --mount-options Version="NFS4_0"
```

The following example command creates an SMB location that DataSync mounts using SMB version 3\.

```
$ aws datasync create-location-smb --server-hostname your-server-address \
   --on-prem-config AgentArns=your-agent-arns \
   --subdirectory smb-export-path \
   --mount-options Version="SMB3"
```

## My task failed with a DataSync currently does not support server\-side NFSv4 ID mapping error<a name="nfs-id-mapping"></a>

This error can occur if a file system involved in your transfer uses NFS version 4 ID mapping, a feature that DataSync doesn't support\.

**Action to take**  
You have a couple options to work around this issue:
+ Create a new DataSync location for the file system that uses NFS version 3\.
+ Disable NFS version 4 ID mapping on the file system\.

Retry the transfer\. Either option should resolve the issue\.

## My task status is unavailable and indicates a mount error<a name="onpremise-location-stuck-mounting"></a>

When you create a task, your task status might transition from **CREATING** to **UNAVAILABLE** when the agent that you chose can't mount the location that you specified during configuration\.

**Action to take**  
First, make sure that the NFS server and export that you specified are both valid\. If they aren't, delete the task, create a new one using the correct NFS server, and then export\. For more information, see [Creating an NFS location](create-locations-cli.md#create-location-nfs-cli)\.

If the NFS server and export are both valid, it generally indicates one of two things\. Either a firewall is preventing the agent from mounting the NFS server, or the NFS server isn't configured to allow the agent to mount it\. 

Make sure that there is no firewall between the agent and the NFS server\. Then make sure that the NFS server is configured to allow the agent to mount the export end specified in the task\. For information about network and firewall requirements, see [AWS DataSync network requirements](datasync-network.md)\.

If you perform these actions and the agent still can't mount the NFS server and export, open a support channel and engage AWS Support\. For information about how to open a support channel, see [Getting help with your agent from AWS Support](local-console-vm.md#enable-support-access)\.

## My task failed with a Cannot allocate memory error<a name="error-cannot-allocate-memory"></a>

When your DataSync task fails with a Cannot allocate memory error, it can mean a few different things\.

**Action to take**  
Try the following until you no longer see the issue:
+ If your transfer involves an agent, make sure that the agent meets the [virtual machine \(VM\) requirements](agent-requirements.md#hardware)\.
+ Split your transfer into multiple tasks using [filters](filtering.md)\. It's possible that you're trying to transfer more files or objects than what [one DataSync task can handle](datasync-limits.md#task-hard-limits)\.
+ If you still see the issue, [contact AWS Support](https://aws.amazon.com/contact-us/)\.

## My task failed with an input/output error<a name="sync-io-error"></a>

You can get an input/output error message if your storage system fails I/O requests from the DataSync agent\. Common reasons for this include a server disk failure, changes to your firewall configuration, or a network router failure\.

If the error involves an NFS server or Hadoop Distributed File System \(HDFS\) cluster, use the following steps to resolve the error\.

**Action to take \(NFS\)**  
First, check your NFS server's logs and metrics to determine if the problem started on the NFS server\. If yes, resolve that issue\.

Next, check that your network configuration hasn't changed\. To check if the NFS server is configured correctly and that DataSync can access it, do the following:

1. Set up another NFS client on the same network subnet as the agent\.

1. Mount your share on that client\.

1. Validate that the client can read and write to the share successfully\.

**Action to take \(HDFS\)**  
Make sure that your HDFS cluster allows the agent to communicate with the cluster's NameNode and DataNode ports\. In most clusters, you can find the port numbers the cluster uses in the following configuration files\.

1. To find the NameNode port, look in the `core-site.xml` file under the `fs.default` or `fs.default.name` property \(depending on the Hadoop distribution\)\.

1. To find the DataNode port, look in the `hdfs-site.xml` file under the `dfs.datanode.address` property\.

## My task has a launching status but nothing seems to be happening<a name="task-stuck-starting"></a>

Your task execution can become stuck in the **Launching** status when DataSync can't instruct the specified source agent to begin a task\. This issue usually occurs because the agent either is powered off or has lost network connectivity\.

**Action to take**  
Make sure that the agent is connected and the status is **ONLINE**\. If the status is **OFFLINE**, then the agent is not connected\. For information about how to test network connectivity, see [Testing your agent's connection to DataSync endpoints](local-console-vm.md#test-network)\.

Next, make sure that your agent is powered on\. If it isn't, power it on\.

If the agent is powered on and the task is still stuck in **LAUNCHING** status, then a network connectivity problem between the agent and DataSync is the most likely issue\. Check your network and firewall settings to make sure that the agent can connect to DataSync\.

If you perform these actions and the issue isn't resolved, open a support channel and engage AWS Support\. For information about how to open a support channel, see [Getting help with your agent from AWS Support](local-console-vm.md#enable-support-access)\.

## My task failed with a permissions denied error<a name="task-permission-denied"></a>

You can get a "permissions denied" error message if you configure your NFS server with `root_squash` or `all_squash` enabled and your files don't have all read access\.

**Action to take**  
To fix this issue, you can configure the NFS export with `no_root_squash`\. Or you can make sure that the permissions for all of the files that you want to transfer allow read access for all users\. Doing either enables the agent to read the files\. For the agent to access directories, you must additionally enable all\-execute access\. 

To make sure that the directory can be mounted, first connect to any computer that has the same network configuration as your agent\. Then run the following CLI command\.

`mount -t nfs -o nfsvers=<your-nfs-server-version> <your-nfs-server-name>:<nfs-export-path-youspecified> <new-test-folder-on-your-computer>`

If you perform these actions and the issue isn't resolved, contact AWS Support\.

## My task has had a preparing status for a long time<a name="Preparing-status-too-long"></a>

The time DataSync spends in the **PREPARING** status depends on the number of files in both the source and destination file systems, and the performance of these file systems\. When a task starts, DataSync performs a recursive directory listing to discover all files and file metadata in the source and destination file system\. These listings are used to identify differences and determine what to copy\. This process usually takes between a few minutes to a few hours\. For more information, see [Starting your DataSync task](run-task.md)\.

**Action to take**  
You shouldn't have to do anything\. Continue to wait for the **PREPARING** status to change to **TRANSFERRING**\. If the status still doesn't change, contact AWS Support\.

## How long does it take to verify a task I've run?<a name="verifying-status-too-long"></a>

The time DataSync spends in the **VERIFYING** status depends on a number of factors\. These are the number of files, the total size of all files in the source and destination file systems, and the performance of these file systems\. By default, **Verification mode** is enabled in the options setting\. The verification DataSync performs includes an SHA256 checksum on all file content and an exact comparison of all file metadata\.

**Action to take**  
You shouldn't have to do anything\. Continue to wait for the **VERIFYING** status to complete\. If the status still doesn't change, contact AWS Support\.

## My task fails when transferring to an S3 bucket in another AWS account<a name="troubleshoot-cross-account-s3"></a>

Unlike DataSync transfers between resources in the same AWS account, copying data to an S3 bucket in a different AWS account requires some extra steps\.
+ **If your DataSync task fails with an error related to S3 bucket permissions**: When creating the task, make sure you're logged in to the AWS Management Console using the same IAM user name \(or role\) which you specified in your destination S3 bucket's policy\. \(Note: This isn't the IAM role that gives DataSync permission to write to the S3 bucket\.\)
+ **If you're also copying data to a bucket in another AWS Region and get an S3 endpoint connection error**: Create the DataSync task in the same Region as the destination S3 bucket\.

For complete instructions on cross\-account transfers with Amazon S3, see the following tutorials:
+ [Transferring data from on\-premises storage to Amazon S3 in a different AWS account](s3-cross-account-transfer.md)
+ [Transferring data from Amazon S3 to Amazon S3 in a different AWS account](tutorial_s3-s3-cross-account-transfer.md)

## My task fails when transferring from a Google Cloud Storage bucket<a name="troubleshoot-object-tags-google-cloud-storage"></a>

Because DataSync communicates with Google Cloud Storage using the Amazon S3 API, there's a limitation that may cause your DataSync task to fail if you try to copy object tags\. The following message related to the issue appears in your CloudWatch Logs:

\[WARN\] Failed to read metadata for file /*your\-bucket*/*your\-object*: S3 Get Object Tagging Failed: proceeding without tagging

To prevent this, deselect the **Copy object tags** option when configuring your task settings\.

## The task execution times don't match up with my logs<a name="troubleshoot-task-exec-times"></a>

The task execution start and end times that you see in the DataSync console may differ between timestamps you see elsewhere related to your transfer\. This is because the console doesn’t take into account the time a task execution spends in the launching or queueing states\.

For example, your Amazon CloudWatch logs can indicate that your task execution ended later than what's displayed in the DataSync console\. You may notice a similar discrepancy in the following areas:
+ Logs for the file system or object storage system involved in your transfer
+ The last modified date on an Amazon S3 object that DataSync wrote to
+ Network traffic coming from the DataSync agent
+ Amazon EventBridge events

## My storage cost is higher than I expected<a name="multipart-upload-policy"></a>

If your storage cost is higher then expected, it might be due to one or more of the following reasons:
+ DataSync uses the Amazon S3 multipart upload feature to upload objects to Amazon S3\. This approach can result in unexpected storage charges for uploads that don't successfully complete\.
+ Object versioning might be enabled on your S3 bucket\. Object versioning results in Amazon S3 storing multiple copies of objects that have the same name\.

**Action to take**  
In these cases, you can take the following steps:
+ If the issue relates to multipart uploads, configure a policy for multipart uploads for your S3 bucket to clean up incomplete multipart uploads to reduce storage cost\. For more information, see the AWS blog post [S3 Lifecycle Management Update \- Support for Multipart Uploads and Delete Markers](http://aws.amazon.com/blogs/aws/s3-lifecycle-management-update-support-for-multipart-uploads-and-delete-markers/)\. 
+ If the issue relates to object versioning, verify whether object versioning is enabled for your Amazon S3 bucket\. If versioning is enabled, turn it off\.

If you perform these actions and the issue isn't resolved, contact AWS Support\. For information about how to contact AWS Support, see [Getting started with AWS Support](https://docs.aws.amazon.com/awssupport/latest/user/getting-started.html)\.