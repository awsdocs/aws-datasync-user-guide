# Using AWS DataSync in a virtual private cloud<a name="datasync-in-vpc"></a>

 You can deploy AWS DataSync in your virtual private cloud \(VPC\) based on the Amazon VPC service by using VPC endpoints\. With this feature, the connection between an agent and the DataSync service doesn't cross the public internet and doesn't require public IP addresses\. These connection restrictions increase the security of your data by keeping network traffic within your VPC\. 

 VPC endpoints for DataSync are powered by VPC endpoint services \(AWS PrivateLink\)\. AWS PrivateLink is a highly available, scalable AWS service that enables you to privately connect your VPC to supported AWS services\. For more information, see [VPC endpoint services \(AWS PrivateLink\)](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-service.html) in the *Amazon VPC User Guide*\. 

 To use VPC endpoints, you can transfer files using AWS Direct Connect or a virtual private network \(VPN\)\. With this kind of transfer, you use private IP addresses that are accessible only from inside your VPC\. 

## How DataSync works with VPC endpoints<a name="working-with-endpoints"></a>

The DataSync agent transfers data between self\-managed storage and AWS\. You deploy the agent as a virtual machine in the same local network as your source storage\. This approach minimizes network overhead associated with transferring data using network protocols such as Network File System \(NFS\) and Server Message Block \(SMB\), or when accessing your self\-managed object storage using the Amazon S3 API\. 

 When you use DataSync with a private VPC endpoint, the DataSync agent can communicate directly with AWS without the need to cross the public internet\. 

## Configuring DataSync to use private IP addresses for data transfer<a name="create-agent-steps-vpc"></a>

 In the following procedure, you can find the steps to configure a DataSync agent and a task that communicate with AWS by using VPC endpoints\. 

 The diagram following illustrates the setup process\. 







**To configure a DataSync agent and task to communicate with AWS by using VPC endpoints**

1. Choose the VPC and subnet where you want to set up the DataSync private IP addresses\. 

   The VPC should extend to your local environment, where your SMB, NFS, or self\-managed object storage is located, by using routing rules over AWS Direct Connect or VPN\. This setup ensures that all communications between the DataSync agent and the DataSync service remain within the VPC\. 

1. Deploy a DataSync agent close to your local storage\. The agent must be able to access your source storage location by using NFS, SMB, or the Amazon S3 API\. You can download the \.ova file for the DataSync agent from the DataSync console\. The agent doesn't need a public IP address\. For more information about downloading and deploying an \.ova image, see [Creating an agent](create-agent-cli.md)\. 
**Note**  
You can use one agent for only one type of endpoint—private, public, or Federal Information Processing Standards \(FIPS\)\. If you already have an agent configured for transferring data over the public internet, deploy a new agent to transfer data to private DataSync endpoints\. For detailed instructions, see [Deploy your DataSync agent](deploy-agents.md)\. 

1. In the VPC that you chose in step 1, create a security group to ensure access to the private IP addresses that DataSync uses\. These addresses include one VPC endpoint for control traffic and four [elastic network interfaces \(ENIs\)](datasync-network.md#required-network-interfaces) to use for data transfer\. You use this security group to manage access to these private IP addresses and ensure that your agent can route to them\. 

   The agent must be able to establish connections to these IP addresses\. In the security group attached to the endpoints, configure inbound rules to allow the agent's private IP address to connect to these endpoints\. 

1.  Create a VPC endpoint for the DataSync service\. 

   To do this, open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/), and choose **Endpoints** from the navigation pane at left\. Choose **Create Endpoint**\. 

   For **Service category**, choose **AWS service**\. For **Service Name**, choose **DataSync** in your AWS Region \(for example, `com.amazonaws.us-east-1.datasync`\)\. Then choose the VPC and security group that you chose in steps 1 and 3\. Make sure that you clear the **Enable Private DNS Name** check box\. 
**Important**  
If you are using a DataSync Amazon EC2 agent, choose the Availability Zone where your agent resides to avoid charges for network traffic between Availability Zones\.  
To learn more about data transfer prices for all AWS Regions, see [Amazon EC2 On\-Demand pricing](http://aws.amazon.com/ec2/pricing/on-demand/)\. 

   For additional details on creating VPC endpoints, see [Creating an interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint) in *Amazon VPC User Guide*\.

1. When your new VPC endpoint becomes available, make sure that the network configuration for your self\-managed environment allows agent activation\. 

    *Activation* is a one\-time operation that securely associates the agent with your AWS account\. To activate the agent, use a computer that can reach the agent by using port 80\. After activation, this access can be revoked\. The agent should be able to reach the private IP address of the VPC endpoint that you created in step 4\. 

   To find this IP address, open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/), and choose **Endpoints** from the navigation pane at left\. Choose the DataSync endpoint, and check the **Subnets** list for the private IP address for the subnet that you chose\. This is the IP address of your VPC endpoint\. 
**Note**  
 Make sure to allow outbound traffic from the agent to the VPC endpoint by using ports 443, 1024–1064, and port 22\. Port 22 is optional and is used for the AWS Support channel\. 

1.  Activate the agent\. If you have a computer that can route to the agent by using port 80 and that can access the DataSync console, open the console and choose **Create Agent**\. In the service endpoint section, choose **VPC endpoints using AWS PrivateLink**\. 

    Choose the VPC endpoint from step 4, the subnet from step 1, and the security group from step 3\. Enter the agent's IP address\. 

   If you can't access the agent and the DataSync console using the same computer, activate the agent using the command line from a computer that can reach the agent's port 80\. For more information, see [Creating an agent](create-agent-cli.md)\. 

1.  Choose **Get Key**, optionally enter an agent name and tags, and choose **Create agent**\. Your new agent now appears on the **Agents** tab of the DataSync console\. The green **VPC Endpoint** banner indicates that all tasks performed with this agent use private endpoints, without crossing the public internet\. 

1.  Create your task by configuring a source and a destination for your data transfer\. For more information on choosing endpoints, see [Choose a service endpoint](choose-service-endpoint.md)\. 

   To make transfer easier by using private IP addresses, your task creates four ENIs in the VPC and subnet that you chose\.

1. Make sure that your agent can reach the four ENIs and related IP addresses that your task creates\.

   To find these IP addresses, open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/), and choose **Network Interfaces** on the dashboard\. Enter the task ID into the search filter to see the task's four ENIs\. These are the ENIs used by your VPC endpoint\. Make sure that you allow outbound traffic from the agent to these interfaces by using port 443\. 

 You can now start your task\. For each additional task that uses this agent, repeat step 9 to allow the task's traffic through port 443\. 