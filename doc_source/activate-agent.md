# Activate your AWS DataSync agent<a name="activate-agent"></a>

After you deploy your AWS DataSync agent and specify a service endpoint that it'll connect to, it's time to activate the agent\. This process associates the agent with your AWS account\.

**Note**  
You can't activate an agent in more than one AWS account and AWS Region at a time\.

**To activate your agent**

1. On the same **Create agent** page, go to the **Activation key** section\.

1. Choose one of the following options to activate your agent:
   + **Automatically get the activation key from your agent** – This option requires that your browser access the agent by using port 80\. Once activated, the agent closes the port\.
     + For **Agent address**, enter the agent's IP address or domain name and choose **Get key**\.

       Your browser connects to the IP address and gets a unique activation key from your agent\. If the activation fails, [check your network configuration](datasync-network.md)\.
   + **Manually enter your agent's activation key** – Use this option if you don't want a connection between your browser and agent\.
     + Get the key from the [agent's local console](local-console-vm.md#get-activation-key)\.
     + Back in the DataSync console, enter the key in the **Activation key** field\.
**Note**  
Agent activation keys expire in 30 minutes if unused\.

1. \(Optional\) For **Agent name**, enter a name for your agent\.

1. \(Optional\) For **Tags**, enter values for the **Key** and **Value** fields to tag your agent\.

   Tags help you manage, filter, and search for your AWS resources\. 

1. Choose **Create agent**\.

   Your agent displays on the **Agents** page\. Verify that your service endpoint is correct\.  
  
  


Once created, AWS manages your agent \(including software updates that don't interrupt your transfers\)\. If needed, you can work with an agent directly using its [local console](local-console-vm.md)\.