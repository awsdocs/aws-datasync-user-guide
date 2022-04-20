# CreateAgent<a name="API_CreateAgent"></a>

Activates an AWS DataSync agent that you have deployed on your host\. The activation process associates your agent with your account\. In the activation process, you specify information such as the AWS Region that you want to activate the agent in\. You activate the agent in the AWS Region where your target locations \(in Amazon S3 or Amazon EFS\) reside\. Your tasks are created in this AWS Region\.

You can activate the agent in a VPC \(virtual private cloud\) or provide the agent access to a VPC endpoint so you can run tasks without going over the public internet\.

You can use an agent for more than one location\. If a task uses multiple agents, all of them need to have status AVAILABLE for the task to run\. If you use multiple agents for a source location, the status of all the agents must be AVAILABLE for the task to run\. 

For more information, see [Creating and activating an agent](https://docs.aws.amazon.com/datasync/latest/userguide/activating-agent.html) in the * AWS DataSync User Guide*\.

Agents are automatically updated by AWS on a regular basis, using a mechanism that ensures minimal interruption to your tasks\.



## Request Syntax<a name="API_CreateAgent_RequestSyntax"></a>

```
{
   "ActivationKey": "string",
   "AgentName": "string",
   "SecurityGroupArns": [ "string" ],
   "SubnetArns": [ "string" ],
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "VpcEndpointId": "string"
}
```

## Request Parameters<a name="API_CreateAgent_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ActivationKey](#API_CreateAgent_RequestSyntax) **   <a name="DataSync-CreateAgent-request-ActivationKey"></a>
Your agent activation key\. You can get the activation key either by sending an HTTP GET request with redirects that enable you to get the agent IP address \(port 80\)\. Alternatively, you can get it from the DataSync console\.  
The redirect URL returned in the response provides you the activation key for your agent in the query string parameter `activationKey`\. It might also include other activation\-related parameters; however, these are merely defaults\. The arguments you pass to this API call determine the actual configuration of your agent\.  
For more information, see [Creating and activating an agent](https://docs.aws.amazon.com/datasync/latest/userguide/activating-agent.html) in the * AWS DataSync User Guide\.*   
Type: String  
Length Constraints: Maximum length of 29\.  
Pattern: `[A-Z0-9]{5}(-[A-Z0-9]{5}){4}`   
Required: Yes

 ** [AgentName](#API_CreateAgent_RequestSyntax) **   <a name="DataSync-CreateAgent-request-AgentName"></a>
The name you configured for your agent\. This value is a text reference that is used to identify the agent in the console\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`   
Required: No

 ** [SecurityGroupArns](#API_CreateAgent_RequestSyntax) **   <a name="DataSync-CreateAgent-request-SecurityGroupArns"></a>
The ARNs of the security groups used to protect your data transfer task subnets\. See [SecurityGroupArns](https://docs.aws.amazon.com/datasync/latest/userguide/API_Ec2Config.html#DataSync-Type-Ec2Config-SecurityGroupArns)\.  
Type: Array of strings  
Array Members: Fixed number of 1 item\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: No

 ** [SubnetArns](#API_CreateAgent_RequestSyntax) **   <a name="DataSync-CreateAgent-request-SubnetArns"></a>
The Amazon Resource Names \(ARNs\) of the subnets in which DataSync will create elastic network interfaces for each data transfer task\. The agent that runs a task must be private\. When you start a task that is associated with an agent created in a VPC, or one that has access to an IP address in a VPC, then the task is also private\. In this case, DataSync creates four network interfaces for each task in your subnet\. For a data transfer to work, the agent must be able to route to all these four network interfaces\.  
Type: Array of strings  
Array Members: Fixed number of 1 item\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:subnet/.*$`   
Required: No

 ** [Tags](#API_CreateAgent_RequestSyntax) **   <a name="DataSync-CreateAgent-request-Tags"></a>
The key\-value pair that represents the tag that you want to associate with the agent\. The value can be an empty string\. This value helps you manage, filter, and search for your agents\.  
Valid characters for key and value are letters, spaces, and numbers representable in UTF\-8 format, and the following special characters: \+ \- = \. \_ : / @\. 
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

 ** [VpcEndpointId](#API_CreateAgent_RequestSyntax) **   <a name="DataSync-CreateAgent-request-VpcEndpointId"></a>
The ID of the VPC \(virtual private cloud\) endpoint that the agent has access to\. This is the client\-side VPC endpoint, also called a PrivateLink\. If you don't have a PrivateLink VPC endpoint, see [Creating a VPC Endpoint Service Configuration](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-service.html#create-endpoint-service) in the Amazon VPC User Guide\.  
VPC endpoint ID looks like this: `vpce-01234d5aff67890e1`\.  
Type: String  
Pattern: `^vpce-[0-9a-f]{17}$`   
Required: No

## Response Syntax<a name="API_CreateAgent_ResponseSyntax"></a>

```
{
   "AgentArn": "string"
}
```

## Response Elements<a name="API_CreateAgent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AgentArn](#API_CreateAgent_ResponseSyntax) **   <a name="DataSync-CreateAgent-response-AgentArn"></a>
The Amazon Resource Name \(ARN\) of the agent\. Use the `ListAgents` operation to return a list of agents for your account and AWS Region\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

## Errors<a name="API_CreateAgent_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_CreateAgent_Examples"></a>

### Example<a name="API_CreateAgent_Example_1"></a>

The following example creates an agent and activates it using an activation key\.

#### Sample Request<a name="API_CreateAgent_Example_1_Request"></a>

```
{
  "ActivationKey": "AAAAA-7AAAA-GG7MC-3I9R3-27COD",
  "AgentName": "MyAgent",
  "Tags": [
  {
    "Key": "Job",
    "Value": "TransferJob-1"
 }
  ]
}
```

### Example<a name="API_CreateAgent_Example_2"></a>

The response returns the Amazon Resource Name \(ARN\) of the activated agent\.

#### Sample Response<a name="API_CreateAgent_Example_2_Response"></a>

```
{ 
  "AgentArn": "arn:aws:datasync:us-east-2:111222333444:agent/agent-0b0addbeef44baca3" 
}
```

## See Also<a name="API_CreateAgent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateAgent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateAgent) 