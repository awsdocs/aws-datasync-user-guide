# Creating an AWS DataSync agent with the AWS CLI<a name="create-agent-cli"></a>

To access your self\-managed storage, you first deploy and activate an AWS DataSync agent\. The activation process associates your agent with your AWS account\. An agent isn't required when transferring between AWS storage services within the same AWS account\. To set up a data transfer between two AWS services, see [Creating AWS DataSync locations with the AWS CLI](create-locations-cli.md)\.

A DataSync agent can transfer data through public service endpoints, Federal Information Processing Standard \(FIPS\) endpoints, and Amazon VPC endpoints\. For more information, see [Creating an AWS DataSync agent](activating-agent.md)\.

**Note**  
When you configure your agent to use Amazon VPC endpoints, the data transferred between your agent and the DataSync service doesn't cross the public internet and doesn't require public IP addresses\. For end\-to\-end instructions for this configuration, see [Using AWS DataSync in a virtual private cloud](datasync-in-vpc.md)\.

**To create an agent to read from a Network File System \(NFS\), Server Message Block \(SMB\), Hadoop Distributed File System \(HDFS\), or self\-managed object storage source location**

1. Download the current DataSync `.ova` image or launch the current DataSync Amazon Machine Image \(AMI\) based on Amazon EC2 from the AWS DataSync console\. For information about how to get the `.ova` image or Amazon EC2 AMI, see [Create an AWS DataSync agent](configure-agent.md)\. For information about hardware requirements and recommended Amazon EC2 instance types, see [Virtual machine requirements](agent-requirements.md#hardware)\.
**Important**  
If you are deploying your agent on Amazon EC2, deploy the agent so that it doesn't require network traffic between Availability Zones \(to avoid charges for such traffic\)\.  
To access your Amazon EFS or Amazon FSx for Windows File Server file system, deploy the agent in an Availability Zone that has a mount target to your file system\.
For self\-managed file systems, deploy the agent in the Availability Zone where your file system resides\.
To learn more about data\-transfer prices for all AWS Regions, see [Amazon EC2 On\-Demand pricing](http://aws.amazon.com/ec2/pricing/on-demand/)\. 

1. Make sure that you satisfy the network\-connectivity requirements for the agent\. For information about network requirements, see [AWS DataSync network requirements](datasync-network.md)\.

1. Deploy the `.ova` image in your hypervisor, power on the hypervisor, and note the agent's IP address\. Make sure that you can reach the agent on port 80\. You can use the following command to check\.

   ```
   nc -vz agent-ip-address 80
   ```
**Note**  
The `.ova` default credentials are login **admin**, password **password**\. You can change the password on the virtual machine \(VM\) local console\. You don't need to log in to the VM for basic DataSync functionality\. Logging in is required mainly for troubleshooting, network\-specific settings, and so on\.  
You log in to the agent VM local console by using your VM's hypervisor client\. For information about how to use the VM local console, see [Working with your DataSync agent's local console](local-console-vm.md)\.

1. Send an HTTP/1\.1 GET request to the agent to get the activation key\. You can do this by using standard Unix tools:
   + To activate an agent by using a public service endpoint, use the following command\.

     ```
     curl "http://agent-ip-address/?gatewayType=SYNC&activationRegion=aws-region&no_redirect"
     ```
   + To activate an agent by using a virtual private cloud \(VPC\) endpoint, use the IP address of the VPC endpoint\. Use the following command\.

     ```
     curl "http://agent-ip-address/?gatewayType=SYNC&activationRegion=aws-region&privateLinkEndpoint=IP address of VPC endpoint&endpointType=PRIVATE_LINK&no_redirect"
     ```

     To find the correct IP address, open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/) and choose **Endpoints** from the navigation pane at left\. Choose the DataSync endpoint, and check **Subnets list** to find the private IP address that corresponds to the subnet that you chose for your VPC endpoint setup\.

     For more information about VPC endpoint configuration, see step 5 in [Configuring DataSync to use private IP addresses for data transfer](datasync-in-vpc.md#create-agent-steps-vpc)\.
   + To activate an agent using a Federal Information Processing Standard \(FIPS\) endpoint, specify `endpointType=FIPS`\. Also, the `activationRegion` value must be set to an AWS Region within the United States\. To activate a FIPS endpoint, use the following command\. 

     ```
     curl "http://agent-IP-address/?gatewayType=SYNC&activationRegion=US-based-aws-region&endpointType=FIPS&no_redirect"
     ```

   This command returns an activation key similar to the one following\.

   `F0EFT-7FPPR-GG7MC-3I9R3-27DOH`

1. After you have the activation key, do one of the following:
   + To activate your agent using a public endpoint or FIPS endpoint, use the following command\.

     ```
     aws datasync create-agent \
       --agent-name agent-name-you-specify \
       --activation-key obtained-activation-key
     ```
   + To activate your agent using a VPC endpoint, use the following command\.

     ```
     aws datasync create-agent \
       --agent-name agent-name-you-specify \
       --vpc-endpoint-id vpc-endpoint-id \
       --subnet-arns subnet-arns \
       --security-group-arns security-group-arns \
       --activation-key obtained-activation-key
     ```

     In this command, use the following arguments:
     + `vpc-endpoint-id` – The AWS endpoint that the agent connects to\. To find the endpoint ID, open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/), and choose **Endpoints** from the navigation pane on the left\. Copy the **Endpoint ID** value of the DataSync endpoint\. For more information about VPC endpoint configuration, see step 5 in [Configuring DataSync to use private IP addresses for data transfer](datasync-in-vpc.md#create-agent-steps-vpc)\.
     + `security-group-arn` – The Amazon Resource Names \(ARNs\) of the security groups to use for the task's endpoint\.

       This is the security group that you created in step 3 of [Configuring DataSync to use private IP addresses for data transfer](datasync-in-vpc.md#create-agent-steps-vpc)\.
     + `subnet-arns` – The ARNs of the subnets where the task endpoints for the agent are created\.

       This is the subnet that you chose in step 1 of [Configuring DataSync to use private IP addresses for data transfer](datasync-in-vpc.md#create-agent-steps-vpc)\.

     These commands return the ARN of the agent that you just activated\. The ARN is similar to the one following\.

     ```
     {
         "AgentArn": "arn:aws:datasync:us-east-1:111222333444:agent/agent-0b0addbeef44baca3”
     }
     ```
**Note**  
After you choose a service endpoint, you can't change it later\.

After you activate the agent, it closes port 80 and the port is no longer accessible\. If you can't connect to the agent after you have activated it, verify that the activation was successful by using the following command:

```
aws datasync list-agents
```

**Note**  
Make sure that you are using the same AWS credentials throughout the whole process\. Don't switch between multiple terminals where you are authenticated with different AWS credentials\.