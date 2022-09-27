# Choose a service endpoint for AWS DataSync<a name="choose-service-endpoint"></a>

You must specify an endpoint that your AWS DataSync agent uses to communicate with AWS\. An agent can connect to the following types of endpoints:
+ **Public service endpoint** – Data is transferred over the public internet\.
+ **Virtual private cloud \(VPC\) endpoint** – Data is transferred within your VPC instead of over the public internet, increasing the security of the copied data\.

  For more information about activating an agent with a private VPC endpoint, see [Using AWS DataSync in a virtual private cloud](datasync-in-vpc.md)\.
+ **Federal Information Processing Standard \(FIPS\) endpoint** – Data is transferred over the public internet by using processes that comply with FIPS\.

**Note**  
After you choose a service endpoint type and activate your agent, you can't change it to use a different service endpoint type later\. If you need to transfer data to multiple endpoint types, create a DataSync agent for each endpoint type that you use\. 

 For more information about service endpoints, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\.

**Topics**
+ [Use a public endpoint](#choose-service-endpoint-public)
+ [Use a VPC endpoint](#choose-service-endpoint-vpc)
+ [Use a FIPS endpoint](#choose-service-endpoint-fips)

## Use a public endpoint<a name="choose-service-endpoint-public"></a>

If you use a public endpoint, all communication from your DataSync agent to AWS occurs over the public internet\. 

**To choose a public service endpoint**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Agents** page and choose **Create agent**\.

1. In the **Service endpoint** section, choose **Public service endpoints in *AWS Region name***\. For a list of supported AWS Regions, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\. 

**Next step: [Activate your AWS DataSync agent](activate-agent.md)**

## Use a VPC endpoint<a name="choose-service-endpoint-vpc"></a>

Your DataSync agent can communicate with AWS using a VPC endpoint \(powered by AWS PrivateLink\)\. This approach provides a private connection between your storage system, your VPC, and AWS services\. 

To use a VPC endpoint outside your VPC, you can use a virtual private network \(VPN\) or AWS Direct Connect\. In this situation, you set up a route table to use the VPC endpoint to access the service\. For more information, see [routing for gateway endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html#vpc-endpoints-routing) in the *AWS PrivateLink Guide*\.

**To use a VPC endpoint**

1. [Create a VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint)\.

   You can use a VPC endpoint in the AWS Region if you already have one\.

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Agents** page and choose **Create agent**\.

1. For **Hypervisor**, choose **Amazon EC2**\.

1. In the **Service endpoint** section, choose **VPC endpoints using AWS PrivateLink**\.

   This is the VPC endpoint that the agent has access to\.  
  
  


1. For **VPC Endpoint**, choose the private VPC endpoint that you want your agent to connect to\.

   You noted the endpoint ID when you created the VPC endpoint\.
**Important**  
You must choose a VPC endpoint that includes the DataSync service name \(for example, `com.amazonaws.us-east-2.datasync`\)\.

1. For **Subnet**, choose the subnet in which you want to run your DataSync task\.

   This is the subnet where the [network interfaces](datasync-network.md#required-network-interfaces) are created\.

1. For **Security Group**, choose a security group for your task\.

   This is the security group that protects your network interface for tasks that run on your agent\.

For additional information about using DataSync in a VPC, see [Using AWS DataSync in a virtual private cloud](datasync-in-vpc.md)\.

**Next step: [Activate your AWS DataSync agent](activate-agent.md)**

## Use a FIPS endpoint<a name="choose-service-endpoint-fips"></a>

If you use a FIPS service endpoint, DataSync communicates with the AWS GovCloud \(US\) or Canada \(Central\) Region\. 

**To choose a FIPS service endpoint**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. For **Hypervisor**, choose the type of agent you deployed\.

1. In the **Service endpoint** section, choose the FIPS endpoint that you want\. For information about supported FIPS endpoint, see [AWS DataSync](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region) in the *AWS General Reference*\.

**Next step: [Activate your AWS DataSync agent](activate-agent.md)**