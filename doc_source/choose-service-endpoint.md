# Choose a service endpoint<a name="choose-service-endpoint"></a>

You must specify an endpoint that your AWS DataSync agent uses to communicate with AWS\. The agent can connect to the following types of endpoints:
+ **Public endpoints**: If you use public endpoints, all communication from your DataSync agent to AWS occurs over the public internet\. For instructions, see [Choose a public service endpoint](#choose-service-endpoint-public)\.
+ **Federal Information Processing Standard \(FIPS\) endpoints**: If you need FIPS 140\-2 validated cryptographic modules when accessing the AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\) Region, use this endpoint to activate your agent\. You use the AWS CLI or API to access this endpoint\. For more information, see [Federal Information Processing Standard \(FIPS\) 140\-2](https://aws.amazon.com/compliance/fips/)\.
+ **Virtual private cloud \(VPC\) endpoints**: If you use a VPC endpoint, all communication from DataSync to AWS occurs through the endpoint in your VPC\. This establishes a private connection between your self\-managed storage system, your VPC, and AWS services, providing extra security as your data is copied over the network\. For instructions, see [Using AWS DataSync in a virtual private cloud](datasync-in-vpc.md)\.

**Note**  
After you choose a service endpoint type and activate your agent, you can't change it to use a different service endpoint type later\. If you need to transfer data to multiple endpoint types, create a DataSync agent for each endpoint type that you use\. 

 For more information about service endpoints, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\.

**Topics**
+ [Choose a public service endpoint](#choose-service-endpoint-public)
+ [Choose a FIPS service endpoint](#choose-service-endpoint-fips)
+ [Choose a VPC endpoint](#choose-service-endpoint-vpc)

## Choose a public service endpoint<a name="choose-service-endpoint-public"></a>

If you use a public endpoint, all communication from your DataSync agent to AWS occurs over the public internet\. 

**To choose a public service endpoint**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Agents** page and choose **Create agent**\.

1. In the **Service endpoint** section, choose **Public service endpoints in *AWS Region name***\. For a list of supported AWS Regions, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\. 

**Next Step: [Activate your agent](activate-agent.md)**

## Choose a FIPS service endpoint<a name="choose-service-endpoint-fips"></a>

If you use a FIPS service endpoint, DataSync communicates with the AWS GovCloud \(US\) or Canada \(Central\) Region\. 

**To choose a FIPS service endpoint**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Agents** page and choose **Create agent**\.

1. In the **Service endpoint** section, choose the FIPS endpoint that you want\. For information about supported FIPS endpoint, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\.

**Next step: [Activate your agent](activate-agent.md)**

## Choose a VPC endpoint<a name="choose-service-endpoint-vpc"></a>

If you use a VPC endpoint, all communication from DataSync to AWS services occurs through the VPC endpoint in your VPC in AWS\. This approach provides a private connection between your self\-managed data center, your VPC, and AWS services\. 

You can also use a VPC endpoint outside your VPC to connect your data center directly to AWS resources\. In this case, you use a virtual private network \(VPN\) or AWS Direct Connect\. You set up a VPC route table to use the endpoint to access the service\. For detailed information, see [Routing for gateway endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html#vpc-endpoints-routing)\.

**To choose a VPC endpoint**

1. Create a VPC endpoint\. For instructions, see [Creating an interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint)\. If you already have a VPC endpoint in the AWS Region, you can use it\.
**Important**  
In step 4 of the instructions mentioned preceding, choose `com.amazonaws.region.datasync` for **Service Name** in the table of endpoints\. For information about supported AWS Regions, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\.

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Agents** page and choose **Create agent**\.

1. In the **Service endpoint** section, choose **VPC endpoints using AWS PrivateLink**\. This is the VPC endpoint that the agent has access to\.  
  
  


1. For **VPC Endpoint**, choose the private VPC endpoint that you want your agent to connect to\. You noted the endpoint ID when you created the VPC endpoint\.

1. For **Subnet**, choose the subnet in which you want to run your task\. This is the subnet where the elastic network interface is created\.

1. For **Security Group**, choose a security group for your task\. This is the security group that protects your network interface for tasks that run on your agent\.

For additional information about using DataSync in a VPC, see [Using AWS DataSync in a virtual private cloud](datasync-in-vpc.md)\.

**Next step: [Activate your agent](activate-agent.md)**