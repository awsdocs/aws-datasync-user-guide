# Tutorial: Transferring data from Google Cloud Storage to Amazon S3<a name="tutorial_transfer-google-cloud-storage"></a>

The following tutorial shows how you can use AWS DataSync to migrate objects from a Google Cloud Storage bucket to an Amazon S3 bucket\.

## Overview<a name="transfer-google-cloud-storage-overview"></a>

Because DataSync integrates with the [Google Cloud Storage XML API](https://cloud.google.com/storage/docs/xml-api/overview), you can copy objects into Amazon S3 without writing code\. How this works depends on where you deploy the DataSync agent that facilitates the transfer\.

------
#### [ Agent in Google Cloud ]

1. You deploy a DataSync agent in your Google Cloud environment\.

1. The agent reads your Google Cloud Storage bucket by using a Hash\-based Message Authentication Code \(HMAC\) key\.

1. The objects from your Google Cloud Storage bucket move securely through TLS 1\.2 into the AWS Cloud by using a public endpoint\.

1. The DataSync service writes the data to your S3 bucket\.

The following diagram illustrates the transfer\.

![\[An example DataSync transfer shows how object data moves from a Google Cloud Storage bucket to an S3 bucket. First, the DataSync agent is deployed in your Google Cloud environment. Then, the DataSync agent reads the Google Cloud Storage bucket. The data moves securely through a public endpoint into AWS, where DataSync writes the objects to an S3 bucket in the same AWS Region where you're using DataSync.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/diagram-transfer-google-cloud-storage-public.png)

------
#### [ Agent in your VPC ]

1. You deploy a DataSync agent in a virtual private cloud \(VPC\) in your AWS environment\.

1. The agent reads your Google Cloud Storage bucket by using a Hash\-based Message Authentication Code \(HMAC\) key\.

1. The objects from your Google Cloud Storage bucket move securely through TLS 1\.2 into the AWS Cloud by using a private VPC endpoint\.

1. The DataSync service writes the data to your S3 bucket\.

The following diagram illustrates the transfer\.

![\[An example DataSync transfer shows how object data moves from a Google Cloud Storage bucket to an S3 bucket. First, the DataSync agent is deployed in a VPC in AWS. Then, the DataSync agent reads the Google Cloud Storage bucket. The data moves securely through a VPC endpoint into AWS, where DataSync writes the objects to an S3 bucket in the same AWS Region as the VPC.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/diagram-transfer-google-cloud-storage.png)

------

## Costs<a name="transfer-google-cloud-storage-cost"></a>

The fees associated with this migration include:
+ Running a Google [Compute Engine](https://cloud.google.com/compute/all-pricing) virtual machine \(VM\) instance \(if you deploy your DataSync agent in Google Cloud\)
+ Running an [Amazon EC2](http://aws.amazon.com/ec2/pricing/) instance \(if you deploy your DataSync agent in a VPC within AWS\)
+ Transferring the data by using [DataSync](http://aws.amazon.com/datasync/pricing/)
+ Transferring data out of [Google Cloud Storage](https://cloud.google.com/storage/pricing)
+ Storing data in [Amazon S3](http://aws.amazon.com/s3/pricing/)

## Prerequisites<a name="transfer-google-cloud-storage-prerequisites"></a>

Before you begin, do the following if you haven’t already:
+ [Create a Google Cloud Storage bucket](https://cloud.google.com/storage/docs/creating-buckets) with the objects that you want to transfer to AWS\.
+ [Create an AWS account](https://portal.aws.amazon.com/billing/signup)\.
+ [Create an Amazon S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) for storing your objects after they're in AWS\.

## Step 1: Create an HMAC key for your Google Cloud Storage bucket<a name="transfer-google-cloud-storage-create-hmac-key"></a>

DataSync uses an HMAC key that's associated with your Google service account to authenticate with and read the bucket that you’re transferring data from\. \(For detailed instructions on how to create HMAC keys, see the [Google Cloud Storage documentation](https://cloud.google.com/storage/docs/authentication/hmackeys)\.\)

**To create an HMAC key**

1. Create an HMAC key for your Google service account\.

1. Make sure that your Google service account has at least `Storage Object Viewer` permissions\.

1. Save your HMAC key's access ID and secret in a secure location\.

   You'll need these items later to configure your DataSync source location\.

## Step 2: Configure your network<a name="transfer-google-cloud-storage-configure-network"></a>

The network requirements for this migration depend on how you want to deploy your DataSync agent\.

### For a DataSync agent in Google Cloud<a name="transfer-google-cloud-storage-configure-public"></a>

If you want to host your DataSync agent in Google Cloud, configure your network to [allow DataSync transfers through a public endpoint](datasync-network.md#using-public-endpoints)\.

### For a DataSync agent in your VPC<a name="transfer-google-cloud-storage-configure-vpc"></a>

If you want to host your agent in AWS, you need a VPC with an interface endpoint\. DataSync uses the VPC endpoint to facilitate the transfer\.

**To configure your network for a VPC endpoint**

1. If you don't have one, [create a VPC](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#Create-VPC) in the same AWS Region as your S3 bucket\.

1. [Create a private subnet for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-subnets.html#create-subnets)\.

1. [Create a VPC endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html) for DataSync by using AWS PrivateLink\.

1. Configure your network to [allow DataSync transfers through a VPC endpoint](datasync-network.md#using-vpc-endpoint)\.

   To make the necessary configuration changes, you can modify the security group that's associated with your VPC endpoint\. For more information, see [Control traffic to resources using security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the *Amazon VPC User Guide*\.

## Step 3: Create a DataSync agent<a name="transfer-google-cloud-storage-create-agent"></a>

You need a DataSync agent that can access and read your Google Cloud Storage bucket\.

### For Google Cloud<a name="transfer-google-cloud-storage-choose-endpoint"></a>

In this scenario, the DataSync agent runs in your Google Cloud environment\.

**Before you begin**: [Install the Google Cloud CLI](https://cloud.google.com/sdk/docs/install)\.

**To create the agent for Google Cloud**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Agents**, then choose **Create agent**\.

1. For **Hypervisor**, choose **VMware ESXi**, then choose **Download the image** to download a `.zip` file that contains the agent\.

1. Open a terminal\. Unzip the image by running the following command:

   ```
   unzip AWS-DataSync-Agent-VMWare.zip
   ```

1. Extract the contents of the agent's `.ova` file beginning with `aws-datasync` by running the following command:

   ```
   tar -xvf aws-datasync-2.0.1655755445.1-x86_64.xfs.gpt.ova
   ```

1. Import the agent's `.vmdk` file into Google Cloud by running the following Google Cloud CLI command:

   ```
   gcloud compute images import aws-datasync-2-test \
      --source-file INCOMPLETE-aws-datasync-2.0.1655755445.1-x86_64.xfs.gpt-disk1.vmdk \
      --os centos-7
   ```
**Note**  
Importing the `.vmdk` file might take up to two hours\.

1. Create and start a VM instance for the agent image that you just imported\. 

   The instance needs the following configurations for your agent\. \(For detailed instructions on how to create an instance, see the [Google Cloud Compute Engine documentation](https://cloud.google.com/compute/docs/instances)\.\)
   + For the machine type, choose one of the following:
     + **e2\-standard\-8** – For DataSync tasks that transfer up to 20 million files\.
     + **e2\-standard\-16** – For DataSync tasks that transfer more than 20 million files\.
   + For the boot disk settings, go to the custom images section\. Then choose the DataSync agent image that you just imported\.
   + For the service account setting, choose your Google service account \(the same account that you used in [Step 1](#transfer-google-cloud-storage-create-hmac-key)\)\.
   + For the firewall setting, choose the option to allow HTTP \(port 80\) traffic\.

     To activate your DataSync agent, port 80 must be open on the agent\. The port doesn't need to be publicly accessible\. Once activated, DataSync closes the port\.

1. After the VM instance is running, take note of its public IP address\.

   You'll need this IP address to activate the agent\.

1. Go back to the DataSync console\. On the **Create agent** screen where you downloaded the agent image, do the following to activate your agent:
   + For **Endpoint type**, choose the public service endpoints option \(for example, **Public service endpoints in US East Ohio**\)\.
   + For **Activation key**, choose **Automatically get the activation key from your agent**\.
   + For **Agent address**, enter the public IP address of the agent VM instance that you just created\.
   + Choose **Get key**\.

1. Give your agent a name, and then choose **Create agent**\.

Your agent is online and ready to move data\.

### For your VPC<a name="transfer-google-cloud-storage-deploy-agent"></a>

In this scenario, the agent runs as an Amazon EC2 instance in a VPC that's associated with your AWS account\.

**Before you begin**: [Set up the AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)\.

**To create the agent for your VPC**

1. Open a terminal\. Make sure to configure your AWS CLI profile to use the account that's associated with your S3 bucket\.

1. Copy the following command\. Replace `vpc-region` with the AWS Region where your VPC resides \(for example, `us-east-1`\)\.

   ```
   aws ssm get-parameter --name /aws/service/datasync/ami --region vpc-region
   ```

1. Run the command\. In the output, take note of the `"Value"` property\.

   This value is the DataSync Amazon Machine Image \(AMI\) ID of the Region that you specified\. For example, an AMI ID could look like `ami-1234567890abcdef0`\.

1. Copy the following URL\. Again, replace `vpc-region` with the AWS Region where your VPC resides\. Then, replace `ami-id` with the AMI ID that you noted in the previous step\.

   ```
   https://console.aws.amazon.com/ec2/v2/home?region=vpc-region#LaunchInstanceWizard:ami=ami-id
   ```

1. Paste the URL into a browser\.

   The Amazon EC2 instance launch page in the AWS Management Console displays\.

1. For **Instance type**, choose one of the [recommended Amazon EC2 instances for DataSync agents](agent-requirements.md#ec2-instance-types)\.

1. For **Key pair**, choose an existing key pair, or create a new one\.

1. For **Network settings**, choose the VPC and subnet where you want to deploy the agent\.

1. Choose **Launch instance**\.

1. After the Amazon EC2 instance is running, [choose your VPC endpoint](choose-service-endpoint.md#choose-service-endpoint-vpc)\.

1. [Activate your agent](activate-agent.md)\.

## Step 4: Create a DataSync source location for your Google Cloud Storage bucket<a name="transfer-google-cloud-storage-create-source"></a>

To set up a DataSync location for your Google Cloud Storage bucket, you need the access ID and secret for the HMAC key that you created in [Step 1](#transfer-google-cloud-storage-create-hmac-key)\.

**To create the DataSync source location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**, then choose **Create location**\.

1. For **Location type**, choose **Object storage**\.

1. For **Agents**, choose the agent that you created in [Step 3](#transfer-google-cloud-storage-create-agent)\.

1. For **Server**, enter **storage\.googleapis\.com**\.

1. For **Bucket name**, enter the name of your Google Cloud Storage bucket\.

1. Expand **Additional settings**\. For **Server protocol**, choose **HTTPS**\. For **Server port**, choose **443**\.

1. Scroll down to the **Authentication** section\. Make sure that the **Requires credentials** check box is selected, and then do the following:
   + For **Access key**, enter your HMAC key's access ID\.
   + For **Secret key**, enter your HMAC key's secret\.

1. Choose **Create location**\.

## Step 5: Create a DataSync destination location for your S3 bucket<a name="transfer-google-cloud-storage-create-destination"></a>

You need a DataSync location for where you want your data to end up\.

**To create the DataSync destination location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**, then choose **Create location**\.

1. [Create a DataSync location for the S3 bucket](create-s3-location.md)\.

   If you deployed the DataSync agent in your VPC, this tutorial assumes that the S3 bucket is in the same AWS Region as your VPC and DataSync agent\. 

## Step 6: Create and start a DataSync task<a name="transfer-google-cloud-storage-start-task"></a>

With your source and destinations locations configured, you can start moving your data into AWS\.

**To create and start the DataSync task**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Tasks**, then choose **Create task**\.

1. On the **Configure source location** page, do the following:

   1. Choose **Choose an existing location**\.

   1. Choose the source location that you created in [Step 4](#transfer-google-cloud-storage-create-source), then choose **Next**\.

1. On the **Configure destination location** page, do the following:

   1. Choose **Choose an existing location**\.

   1. Choose the destination location that you created in [Step 5](#transfer-google-cloud-storage-create-destination), then choose **Next**\.

1. On the **Configure settings** page, do the following:

   1. Under **Data transfer configuration**, expand **Additional settings** and clear the **Copy object tags** check box\.
**Important**  
If you try to copy object tags, your DataSync task might fail\. For more information, see [Considerations when migrating to or from a Google Cloud Storage bucket](create-object-location.md#object-storage-considerations)\.

   1. Configure any other task settings that you want, and then choose **Next**\.

1. On the **Review** page, review your settings, and then choose **Create task**\.

1. On the task's details page, choose **Start**, and then choose one of the following:
   + To run the task without modification, choose **Start with defaults**\.
   + To modify the task before running it, choose **Start with overriding options**\.

When your task finishes, you'll see the objects from your Google Cloud Storage bucket in your S3 bucket\.