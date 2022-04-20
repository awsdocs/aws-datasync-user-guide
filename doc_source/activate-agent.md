# Activate your agent<a name="activate-agent"></a>

After you deploy your AWS DataSync agent and specify a service endpoint, you must activate the agent to associate it with your AWS account\.

**Note**  
An agent can be associated with only one AWS account at a time\.

**To activate your agent**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Agents** page and choose **Create agent**\.

1. In the **Activation key** section, select **Automatically get the activation key from your agent**\.

   This option requires that your browser access the agent using port 80\. Once activated, the agent closes the port\. For more information, see [Network requirements](datasync-network.md)\.

   Alternatively, select **Manually enter your agent's activation key** if you don't want a connection between your browser and agent\. For more information, see [Obtaining an activation key using the local console](local-console-vm.md#get-activation-key)\.

1. For the **Agent address**, enter the agent's IP address or domain name and select **Get key**\. Your browser connects to the IP address and gets a unique activation key from your agent\. 

   If activation succeeds, the activation key is displayed\. If the activation fails, make sure that your security group is configured properly and verify that your firewall allows the required ports\.

1. \(Optional\) For **Agent name**, enter a name for your agent\.

1. \(Optional\) For **Tags**, enter a key and value to add a tag to your agent\. A *tag* is a key\-value pair that helps you manage, filter, and search for your agents\. 

1. Choose **Create agent**\. Your agent is listed on the **Agents** page\. In the **Service endpoint** column, verify that your service endpoint is correct\.  
  
  


1. In the **Tasks** section of the page, choose **Create task**\. The **Configure source location** page appears\.