# Creating and activating a DataSync agent<a name="activating-agent"></a>

After you deploy your agent in your on\-premises hypervisor or Amazon EC2 environment, you must activate the agent\. 

Activate your agent in the AWS Region where the Amazon S3 bucket, Amazon EFS file system, Amazon FSx for Windows File Server file system, Amazon FSx for Lustre file system, or Amazon FSx for OpenZFS file system that you plan to use with AWS DataSync resides\. The activation process associates your agent with your AWS account in the most secure way available\. An agent can be associated with only one AWS account at a time\.

All network traffic transferred between the agent and AWS is encrypted with Transport Layer Security \(TLS\)\. A DataSync agent can communicate with AWS by connecting to one of the following types of endpoints:
+ **Public service endpoint** – Data transfers over the public internet\.
+ **Private virtual private cloud \(VPC\) endpoint** – Data transfers within your VPC instead of the public internet, increasing the security of the copied data\.

  For more information about activating an agent with a private VPC endpoint, see [Using AWS DataSync in a virtual private cloud](datasync-in-vpc.md)\.
+ **Federal Information Processing Standard \(FIPS\) endpoint** – Data transfers over the public internet using processes that comply with FIPS\.

Your agent is managed by AWS, which automatically updates the agent without interrupting your tasks\. To access the agent's local console, see [Logging in to the agent local console](local-console-vm.md#local-console-login)\.

For the agent to work properly, make sure that your network is configured properly\. For information about network requirements, see [Network requirements](datasync-network.md)\. You can use the virtual machine's \(VM's\) local console to test for internet connectivity\. For more information, see [Testing your agent connection to DataSync endpoints](local-console-vm.md#test-network)\.

In some cases, an agent is activated but isn't functioning properly\. This issue can come from problems with a network partition, firewall misconfiguration, or other events that prevent the agent VM from connecting to AWS\. For information about how to troubleshoot connectivity and activation issues, see [Testing your agent connection to DataSync endpoints](local-console-vm.md#test-network)\.

For instructions on how to create an agent on a VMware ESXi host, see [Deploy your agent on VMware](deploy-agents.md#create-vmw-agent)\.

For instructions on how to create an agent on a KVM host, see [Deploy your agent on KVM](deploy-agents.md#create-kvm-agent)\.

For instructions on how to create an agent on a Microsoft Hyper\-V host, see [Deploy your agent on Hyper\-V](deploy-agents.md#create-hyper-v-agent)\.

For instructions on how to create an agent on an Amazon EC2 instance, see [Deploy your agent as an Amazon EC2 instance](deploy-agents.md#ec2-deploy-agent)\.