# Creating an AWS DataSync agent<a name="activating-agent"></a>

AWS DataSync provides several types of agents for different storage environments\. For example, you can use a VMware agent to transfer data from an on\-premises file system\. If you're copying data from a cloud\-based file share that isn't an AWS storage service, you must deploy your DataSync agent as an Amazon EC2 instance\.

**Tip**  
You don't need an agent to copy data between AWS storage services\.

Creating an agent involves the following steps:

1. [Configure your network](datasync-network.md) so that your agent can communicate with your storage system and AWS\.

1. [Deploy your agent](deploy-agents.md) as close to your storage system as possible\.

1. [Choose a service endpoint](choose-service-endpoint.md) that your agent uses to communicate with AWS\.

1. [Activate your agent](activate-agent.md)\.