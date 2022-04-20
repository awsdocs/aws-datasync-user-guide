# Deploy your DataSync agent<a name="deploy-agents"></a>

Where you deploy your AWS DataSync agent depends on where you're copying data to and from and whether you're working with on\-premises or in\-cloud storage systems\.

**Topics**
+ [Deploy your agent on VMware](#create-vmw-agent)
+ [Deploy your agent on KVM](#create-kvm-agent)
+ [Deploy your agent on Hyper\-V](#create-hyper-v-agent)
+ [Deploy your agent as an Amazon EC2 instance](#ec2-deploy-agent)
+ [Deploy your agent on AWS Snowcone](#snowcone-agent)
+ [Deploy your agent on AWS Outposts](#outposts-agent)

## Deploy your agent on VMware<a name="create-vmw-agent"></a>

You can download and deploy an AWS DataSync agent in your VMware environment and then activate it\. You can also use an existing agent instead of deploying a new one\. You can use a previously created agent if it can access your self\-managed storage and if it's activated in the same AWS Region\.

**To deploy an agent on VMware**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. If you don't have an agent, on the **Create agent** page in the console, choose **Download image** in the **Deploy agent** section\. Doing this downloads the agent and deploys it in your VMware ESXi hypervisor\. The agent is available as a VM\. If you want to deploy the agent as an Amazon EC2 instance, see [Deploy your agent as an Amazon EC2 instance](#ec2-deploy-agent)\.

   AWS DataSync currently supports the VMware ESXi hypervisor\. For information about hardware requirements for the VM, see [Virtual machine requirements](agent-requirements.md#hardware)\. For information about how to deploy an `.ova` file in a VMware host, see the documentation for your hypervisor\.

   If you have previously activated an agent in this AWS Region and want to use that agent, choose that agent and choose **Create agent**\. The [Configure a source location](configure-source-location.md) page appears\.

1. Power on your hypervisor, log in to your VM, and get the IP address of the agent\. You need this IP address to activate the agent\.
**Note**  
The VM's default credentials are the login **admin** and the password **password**\.   
You can change the password on the local console\. You don't need to log in to the VM for DataSync functionality\. Login is mainly required for troubleshooting, such as running a connectivity test or opening a support channel with AWS\. It's also required for network\-specific settings, such as setting up a static IP address\. 

After you have deployed an agent, you [choose a service endpoint](choose-service-endpoint.md)\.

## Deploy your agent on KVM<a name="create-kvm-agent"></a>

You can download and deploy an AWS DataSync agent in your KVM environment and then activate it\. You can also use an existing agent instead of deploying a new one\. You can use a previously created agent if it can access your self\-managed storage and if it's activated in the same AWS Region\.

**To deploy an agent on KVM**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. If you don't have an agent, on the **Create agent** page in the console, choose** Download image** in the **Deploy agent** section\. Doing this downloads the agent in a `.zip` file that contains a `.qcow2` image file that can you can deploy in your KVM hypervisor\. 

   The agent is available as a VM\. If you want to deploy the agent as an Amazon EC2 instance, see [Deploy your agent as an Amazon EC2 instance](#ec2-deploy-agent)\.

   AWS DataSync currently supports the KVM hypervisor\. For information about hardware requirements for the VM, see [Virtual machine requirements](agent-requirements.md#hardware)\.

   To get started installing your `.qcow2` image for use in KVM, use the following command\. 

   ```
   virt-install \
   --name "datasync" \
   --description "AWS DataSync agent" \
   --os-type=generic \
   --ram=32768 \
   --vcpus=4 \
   --disk path=datasync-yyyymmdd-x86_64.qcow2,bus=virtio,size=80 \
   --network default,model=virtio \
   --graphics none \
   --import
   ```

    For information about how to manage this VM, and your KVM host, see the documentation for your hypervisor\. 

   If you previously activated an agent in this AWS Region and want to use that agent, choose that agent, and then choose **Create agent**\. The [Configure a source location](configure-source-location.md) page appears\.

1. Power on your hypervisor, log in to your VM, and get the IP address of the agent\. You need this IP address to activate the agent\.
**Note**  
The VM's default credentials are the login **admin** and the password **password**\.   
You can change the password on the local console\. You don't need to log in to the VM for DataSync functionality\. Login is mainly required for troubleshooting, such as running a connectivity test or opening a support channel with AWS\. It's also required for network\-specific settings, such as setting up a static IP address\. 

After you deploy an agent, you [choose a service endpoint](choose-service-endpoint.md)\.

## Deploy your agent on Hyper\-V<a name="create-hyper-v-agent"></a>

You can download and deploy an AWS DataSync agent in your Hyper\-V environment and then activate it\. You can also use an existing agent instead of deploying a new one\. You can use a previously created agent if it can access your self\-managed storage and if it's activated in the same AWS Region\.

**To deploy an agent on Hyper\-V**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. If you don't have an agent, on the **Create agent** page in the console, choose **Download image** in the **Deploy agent** section\. Doing this downloads the agent in a `.zip` file that contains a `.vhdx` image file that can you can deploy in your Hyper\-V hypervisor\. 

   The agent is available as a VM\. If you want to deploy the agent as an Amazon EC2 instance, see [Deploy your agent as an Amazon EC2 instance](#ec2-deploy-agent)\.

   AWS DataSync currently supports the Hyper\-V hypervisor\. For information about hardware requirements for the VM, see [Virtual machine requirements](agent-requirements.md#hardware)\. For information about how to deploy a `.vhdx` file in a Hyper\-V host, see the documentation for your hypervisor\.

   If you previously activated an agent in this AWS Region and want to use that agent, choose that agent, and then choose **Create agent**\. The [Configure a source location](configure-source-location.md) page appears\.

1. Power on your hypervisor, log in to your VM, and get the IP address of the agent\. You need this IP address to activate the agent\.
**Note**  
The VM's default credentials are the login **admin** and the password **password**\.   
You can change the password on the local console\. You don't need to log in to the VM for DataSync functionality\. Login is mainly required for troubleshooting, such as running a connectivity test or opening a support channel with AWS\. It's also required for network\-specific settings, such as setting up a static IP address\. 

After you deploy an agent, you [choose a service endpoint](choose-service-endpoint.md)\.

## Deploy your agent as an Amazon EC2 instance<a name="ec2-deploy-agent"></a>

You deploy a DataSync agent as an Amazon EC2 instance when copying data between:
+ A self\-managed, in\-cloud storage system and an AWS storage service\. 

  For more information about these use cases, including high\-level architecture diagrams, see [Deploying your DataSync agent in AWS Regions](using-ec2-agent-in-region.md)\. 
+ [Amazon S3 on AWS Outposts](#outposts-agent) and an AWS storage service\.

**Warning**  
We don't recommend using an Amazon EC2 agent to access your on\-premises storage because of increased network latency\. Instead, deploy the agent as a VMware, KVM, or Hyper\-V virtual machine in your data center as close to your on\-premises storage as possible\. 

**To choose the agent AMI for your AWS Region**<a name="AMI-command"></a>
+ Use the following CLI command to get the latest DataSync Amazon Machine Image \(AMI\) ID for the specified AWS Region\.

  ```
  aws ssm get-parameter --name /aws/service/datasync/ami --region $region
  ```  
**Example command and output**  

  ```
  aws ssm get-parameter --name /aws/service/datasync/ami --region us-east-1                              
  
  {
      "Parameter": {
          "Name": "/aws/service/datasync/ami",
          "Type": "String",
          "Value": "ami-id",
          "Version": 6,
          "LastModifiedDate": 1569946277.996,
          "ARN": "arn:aws:ssm:us-east-1::parameter/aws/service/datasync/ami"
      }
  }
  ```

  For the recommended instance types, see [Amazon EC2 instance requirements](agent-requirements.md#ec2-instance-types)\. 

  If you activate an agent in the Region that has access to your file system using a mount target in the same Availability Zone and you want to use that agent, choose the agent and select choose **Create agent**\. The [Configure a source location](configure-source-location.md) page appears\. <a name="efs-efs-steps"></a>

**To deploy your DataSync agent as an Amazon EC2 instance**
**Important**  
To avoid charges, deploy your agent in a way that it doesn't require network traffic between Availability Zones\. For example, deploy your agent in the Availability Zone where your self\-managed file system resides\.  
To learn more about data transfer prices for all AWS Regions, see [Amazon EC2 On\-Demand pricing](http://aws.amazon.com/ec2/pricing/on-demand/)\. 

1. From the AWS account where the source file system resides, launch the agent using your AMI from the Amazon EC2 launch wizard\. Use the following URL to launch the AMI\.

   ```
   https://console.aws.amazon.com/ec2/v2/home?region=source-file-system-region#LaunchInstanceWizard:ami=ami-id
   ```

   In the URL, replace the` source-file-system-region` and `ami-id` with your own source AWS Region and AMI ID\. The **Choose an Instance Type** page appears on the Amazon EC2 console\. To find the DataSync AMI ID for a specified AWS Region, use the [.AMI-command](#AMI-command) CLI command described in the preceding section\.

1. Choose one of the recommended instance types for your use case, and choose ****Next**: Configure Instance Details**\. For the recommended instance types, see [Amazon EC2 instance requirements](agent-requirements.md#ec2-instance-types)\.

1. On the **Configure Instance Details** page, do the following:

   1. For **Network**, choose the virtual private cloud \(VPC\) where your source Amazon EFS or NFS file system is located\.

   1. For **Auto\-assign Public IP**, choose a value\. For your instance to be accessible from the public internet, set **Auto\-assign Public IP** to **Enable**\. Otherwise, set** Auto\-assign Public IP** to **Disable**\. If a public IP address isn't assigned, activate the agent in your VPC using its private IP address\.

      When you transfer files from an in\-cloud file system, to increase performance we recommend that you choose a **Placement Group** value where your NFS server resides\.

1. Choose **Next: Add Storage**\. The agent doesn't require additional storage, so you can skip this step and choose **Next: Add tags**\.

1. \(Optional\) On the **Add Tags** page, you can add tags to your Amazon EC2 instance\. When you're finished on the page, choose** Next: Configure Security Group**\.

1. On the **Configure Security Group** page, do the following:

   1. Make sure that the selected security group allows inbound access to HTTP port 80 from the web browser that you plan to use to activate the agent\.

   1. Make sure that the security group of the source file system allows inbound traffic from the agent\. In addition, make sure that the agent allows outbound traffic to the source file system\. If you deploy your agent using a VPC endpoint, you need to allow additional ports\. For more information, see [How DataSync works with VPC endpoints ](datasync-in-vpc.md#working-with-endpoints)\.

   For the complete set of network requirements for DataSync, see [Network requirements](datasync-network.md)\.

1. Choose **Review and Launch** to review your configuration, then choose **Launch** to launch your instance\. Remember to use a key pair that's accessible to you\. A confirmation page appears and indicates that your instance is launching\.

1. Choose **View Instances** to close the confirmation page and return to the Amazon EC2 instances screen\. When you launch an instance, its initial state is **pending**\. After the instance starts, its state changes to **running**\. At this point, it's assigned a public Domain Name System \(DNS\) name and IP address, you can find these in the **Descriptions** tab\.

1. If you set **Auto\-assign Public IP** to **Enable**, choose your instance and note the public IP address in the **Description** tab\. You use this IP address later to connect to your sync agent\. 

   If you set **Auto\-assign Public IP** to **Disable**, launch or use an existing instance in your VPC to activate the agent\. In this case, you use the private IP address of the sync agent to activate the agent from this instance in the VPC\.

## Deploy your agent on AWS Snowcone<a name="snowcone-agent"></a>

The DataSync agent AMI is pre\-installed on your Snowcone device\. Launch the agent with one of the following tools:
+ [AWS OpsHub](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/use-data-sync.html)
+ [Snowball Edge client](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/snowcone-using-client-commands.html#snowcone-launch-ds-ami)

## Deploy your agent on AWS Outposts<a name="outposts-agent"></a>

You can launch a DataSync Amazon EC2 instance on your AWS Outpost\. To learn more about launching an AMI on AWS Outposts, see [Launch an instance on your Outpost](https://docs.aws.amazon.com/outposts/latest/userguide/launch-instance.html) in the *AWS Outposts User Guide*\. 

When using DataSync to access Amazon S3 on Outposts, you must launch the agent in a VPC that's allowed to access your Amazon S3 access point, and activate the agent in the Outpost's parent Region\. The agent must also be able to route to the Amazon S3 on Outposts endpoint for the bucket\. To learn more about working with Amazon S3 on Outposts endpoints, see [Working with Amazon S3 on Outposts](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WorkingWithS3Outposts.html#AccessingS3Outposts) in the *Amazon S3 User Guide*\.