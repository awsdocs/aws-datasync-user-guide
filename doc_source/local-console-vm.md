# Working with your DataSync agent's local console<a name="local-console-vm"></a>

If you deployed your AWS DataSync agent on\-premises, you can troubleshoot issues with the agent using the VM's local console\. For example, you'll log in to the console if you need to run a connectivity test or open a support channel with AWS\.

**Note**  
You don't need to use the agent's local console for standard DataSync functionality\.

**Topics**
+ [Logging in to the agent local console](#local-console-login)
+ [Obtaining an activation key using the local console](#get-activation-key)
+ [Configuring your agent network settings](#network-configration)
+ [Testing your agent connection to DataSync endpoints](#test-network)
+ [Testing connectivity to self\-managed storage](#self-managed-storage-connectivity)
+ [Viewing your agent system resource status](#system-resource-check)
+ [Configuring a Network Time Protocol \(NTP\) server for VMware agents](#time-management)
+ [Running AWS DataSync commands on the local console](#command-prompts)
+ [Enabling AWS Support to help troubleshoot your running agent](#enable-support-access)

## Logging in to the agent local console<a name="local-console-login"></a>

For security reasons, you can't remotely connect to the local console of the DataSync agent VM\. 

**To log in to the agent's local console**
+ If this is your first time using the local console, log in with the default credentials\. The default user name is **admin** and the password is **password**\. Otherwise, use your credentials to log in\.
**Note**  
We recommend changing the default password\. You do this by running the `passwd` command from the local console menu\. \(Item **5** on the main menu opens the command prompt\. For VMware VMs, choose item **6**\.\) For information about how to run the command, see [Running AWS DataSync commands on the local console](#command-prompts)\. 

## Obtaining an activation key using the local console<a name="get-activation-key"></a>

If your agent isn't activated yet, you can obtain its activation key from the local console\. This option is displayed only until the agent has been activated\.

**To get an activation key for your agent from the local console**

1. Log in to your agent's local console\.

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **0** to get an activation key\.

1. Enter the AWS Region that your agent will be activated in\.

1. Enter the service endpoint type that your agent will be using\. Options include public, Federal Information Processing Standard \(FIPS\), and virtual private cloud \(VPC\) with AWS PrivateLink\.

1. The activation key is automatically generated and displayed on screen\. Select and copy this value\.

1. Using the activation key copied from the last step, use the following CLI command to create and activate the agent:

   ```
   $ aws datasync create-agent --agent-name your-new-agent-name --activation-key generated-activation-key
   ```

   On successful activation, this command returns something similar to the following\.

   ```
   {
   "AgentArn": "arn:aws:datasync:us-west-1:1234567890A:agent/agent-ID"
   }
   ```

   You can also insert the activation key in the DataSync console using the agent creation wizard\.

   After the agent is activated, the console menu displays the **Agent ID** and **AWS Region**\. The option for getting an activation key is no longer visible in the console menu\. 

## Configuring your agent network settings<a name="network-configration"></a>

The default network configuration for the agent is Dynamic Host Configuration Protocol \(DHCP\)\. With DHCP, your agent is automatically assigned an IP address\. In some cases, you might need to manually assign your agent's IP as a static IP address, as described following\.

**To configure your agent to use static IP addresses**

1. Log in to your agent's local console

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **1** to begin configuring your network\.

1. On the ** Network Configuration** menu, choose one of the following options\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/local-console-vm.html)

## Testing your agent connection to DataSync endpoints<a name="test-network"></a>

You can use your agent's local console to test your internet connection\. This test can be useful when you are troubleshooting network issues with your agent\.

**To test your agent's connection to AWS DataSync endpoints**

1. Log in to your agent's local console\.

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **2** to begin testing network connectivity\.

1. Enter the service endpoint type that your agent is connecting to\. Valid endpoint types include public, FIPS, and VPC endpoints using AWS PrivateLink\.

   When the agent is activated, the **Test Network Connectivity** option can be initiated without any additional user input, because the Region and endpoint type are taken from the activated agent information\.

   1. To test public endpoint connectivity, enter **1**, followed by the AWS Region in which your agent is activated\. Connectivity test results against the correct endpoints for your agent's Region are displayed\. For information about AWS Regions and endpoints, see [Where can I use DataSync?](setting-up.md#datasync-regions)\.

      Each endpoint in the selected AWS Region displays either a **PASSED** or **FAILED** message\.

   1. To test FIPS endpoint connectivity, enter **2**, followed by the AWS Region in which your agent is activated\. Connectivity test results against the correct endpoints for your agent's Region are displayed\. For information about AWS Regions and endpoints, see [Where can I use DataSync?](setting-up.md#datasync-regions)\.

      Each endpoint in the selected AWS Region displays either a **PASSED** or **FAILED** message\.

   1. To test VPC connectivity, enter **3**\. Network connectivity test results for your agent's VPC endpoints are displayed\.

      Each VPC endpoint displays either a **PASSED** or **FAILED** message\.

For information about network and firewall requirements, see [Network requirements](datasync-network.md)\.

## Testing connectivity to self\-managed storage<a name="self-managed-storage-connectivity"></a>

You can use the console to test connectivity to your self\-managed storage, including Network File System \(NFS\), Server Message Block \(SMB\), Hadoop Distributed File System \(HDFS\), or object storage servers\.

**To test connectivity to self\-managed storage servers**

1. Log in to your agent's local console\.

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **3** to begin testing network connectivity of self\-managed storage\.

1. Choose the location type for connectivity testing\. Options include the following\.

   1. Enter **1** to test connectivity to an NFS server\.

   1. Enter **2** to test connectivity to an SMB server\.

   1. Enter **3** to test connectivity to an object storage server\.

   1. Enter **4** to test connectivity to HDFS\.

   Enter the IP address or server domain name of the self\-managed storage\. For HDFS, enter the IP address or hostname of the NameNode or DataNode in the Hadoop cluster, followed by the TCP port number\. 

   Connectivity test results, either **PASSED** or **FAILED**, are displayed for the specified server, along with the IP address and port of the tested server\.

## Viewing your agent system resource status<a name="system-resource-check"></a>

When you log in to your agent console, virtual CPU cores, root volume size, and RAM are automatically checked\. If there are any errors or warnings, they're flagged on the console menu display with a banner that provides details about those errors or warnings\.

If there are no errors or warnings when the console starts, the menu displays white text\. The **View System Resource Check** option will display `(0 Errors)`\.

If there are errors or warnings, the console menu displays the number of errors and warnings, in red and yellow respectively, in a banner across the top of the menu\. For example, `(1 ERROR, 1 WARNING)`\.

**To view the status of a system resource check**

1. Log in to your agent's local console\.

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **4** to view the results of the system resource check\.

   The console displays an **\[OK\]**, **\[WARNING\]**, or **\[FAIL\]** message for each resource as described in the table following\.

   For Amazon EC2 instances, the system resource check verifies that the instance type is one of the instances recommended for use with DataSync\. If the instance type matches that list, a single result is displayed in green text, as follows\.

   `[ OK ] Instance Type Check`

   If the Amazon EC2 instance is not on the recommended list, the system resource check verifies the following resources\.
   + CPU cores check: At least four cores are required\.
   + Disk size check: A minimum of 80 GB of available disk space is required\.
   + RAM check: A minimum of 32 GiB of RAM is required for up to 20 million file transfers per task\. A minimum of 64 GiB of RAM is required for more than 20 million file transfers per task\.
   + CPU flags check: The agent VM CPU must have either SSSE3 or SSE4 instruction set flags\.

   If the Amazon EC2 instance is not on the list of recommended instances for DataSync, but it has sufficient resources, the result of the system resource check displays four results, all in green text\.

   The same resources are verified for agents deployed in Hyper\-V, Linux Kernel\-based Virtual Machine \(KVM\), and VMware VMs\.

   VMware agents are also checked for supported version; unsupported versions trigger a red banner error\. Supported versions include VMware versions 6\.5 and 6\.7\.

## Configuring a Network Time Protocol \(NTP\) server for VMware agents<a name="time-management"></a>

If you are using a VMware VM, you can view Network Time Protocol \(NTP\) server configurations and synchronize the VM time on your agent with your VMware hypervisor host\.

**To manage system time**

1. Log in to your agent's local console\.

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **5** to manage your system's time\.

1. On the **System Time Management** menu, enter **1** to view and synchronize the VM system time\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/local-console-vm.html)

## Running AWS DataSync commands on the local console<a name="command-prompts"></a>

The VM local console in AWS DataSync helps provide a secure environment for configuring and diagnosing issues with your agent\. Using the local console commands, you can perform maintenance tasks such as saving routing tables, connecting to AWS Support, and so on\.

**To run a configuration or diagnostic command**

1. Log in to your agent's local console\.

1. On the **AWS DataSync Activation \- Configuration** main menu, enter **5** for **Command Prompt**\.
**Note**  
If you are using a VMware VM, enter **6** for the **Command Prompt**\.

1. The commands available to be used through the console include the following\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/local-console-vm.html)

1. At the command prompt, enter the command that you want to use and follow the instructions\.

## Enabling AWS Support to help troubleshoot your running agent<a name="enable-support-access"></a>

You can allow AWS Support to access your AWS DataSync agent and assist you with troubleshooting agent issues\. By default, AWS Support access to DataSync is disabled\. You enable this access through the host's local console\. To give AWS Support access to DataSync, you first log in to the local console for the host and then connect to the support server\.

To log in to an agent running on Amazon EC2, create a rule for the instance's security group that opens TCP port 22 for Secure Shell \(SSH\) access\.

**Note**  
If you add a new rule to an existing security group, the new rule applies to all instances that use that security group\. For more information about security groups and how to add a security group rule, see [Amazon EC2 security groups for Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) in the *Amazon EC2 User Guide for Linux Instances\.*

**To enable AWS Support access to AWS DataSync**

1. Log in to your host's local console\.

   If this is your first time logging in to the local console, see [Logging in to the agent local console](#local-console-login)\.

1. At the prompt, enter **5** to open the command prompt \(for VMware VMs, use **6**\)\.

1. Enter **h** to open the **AVAILABLE COMMANDS** window\.

1. In the **AVAILABLE COMMANDS** window, enter the following to connect to AWS Support:

   `open-support-channel`

   If you are using the agent with VPC endpoints, you must provide a VPC endpoint IP address for your support channel, as follows: 

   `open-support-channel vpc-ip-address`

   Your firewall must allow the outbound TCP port 22 to initiate a support channel to AWS\. When you connect to AWS Support, DataSync assigns you a support number\. Make a note of your support number\.
**Note**  
The channel number is not a Transmission Control Protocol/User Datagram Protocol \(TCP/UDP\) port number\. Instead, it makes a Secure Shell \(SSH\) \(TCP 22\) connection to servers and provides the support channel for the connection\.

1. When the support channel is established, provide your support service number to AWS Support so that they can provide troubleshooting assistance\. 

1. When the support session is finished, press **Enter** to end it\.

1. Enter **exit** to log out of the DataSync local console\.

1. Follow the prompts to exit the local console\.