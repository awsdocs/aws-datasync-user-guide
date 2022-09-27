# Getting started with AWS DataSync Discovery<a name="discovery-getting-started"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

Before you begin, you must make sure that your on\-premises storage system meets AWS DataSync Discovery requirements\. You also must create a DataSync agent that can connect with your storage system\.

## Requirements<a name="discovery-prerequisites"></a>
+ DataSync Discovery currently supports NetApp Fabric\-Attached Storage \(FAS\) and All Flash FAS \(AFF\) systems that are running ONTAP 9\.8 or later\.
+ The [agent](#discovery-create-agent) that you use with DataSync Discovery must have 80 GB of disk space and 16 GB of RAM\.

## Create an agent<a name="discovery-create-agent"></a>

DataSync Discovery connects to the management interface of your on\-premises storage system by using a DataSync agent\. 

**Note**  
We recommend that you use this agent only with DataSync Discovery\. To transfer data with DataSync, create a separate agent\.

The process to create an agent includes:

1. Deploying an agent where it can access your on\-premises storage system\.

1. Configuring your network in the following manner:
   + Allow traffic from your agent to [public service endpoints](datasync-network.md#using-public-endpoints)\. \(DataSync Discovery only supports public service endpoints at this time\.\)
   + Allow traffic from your agent to your storage system's management interface port\. \(You specify this port when [adding the storage system](discovery-configure-storage.md) to DataSync Discovery\.\)
   + Allow traffic between your agent and the `discovery-datasync.us-east-1.amazonaws.com` endpoint on TCP port 443 \(HTTPS\)\.

1. Activating your agent using the public service endpoint in the US East \(N\. Virginia\) Region \(`us-east-1`\)\.
**Note**  
DataSync Discovery currently only supports the US East \(N\. Virginia\) Region\.

For detailed steps, see [Create an AWS DataSync agent](configure-agent.md)\. 