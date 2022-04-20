# DescribeAgent<a name="API_DescribeAgent"></a>

Returns metadata such as the name, the network interfaces, and the status \(that is, whether the agent is running or not\) for an agent\. To specify which agent to describe, use the Amazon Resource Name \(ARN\) of the agent in your request\. 

## Request Syntax<a name="API_DescribeAgent_RequestSyntax"></a>

```
{
   "AgentArn": "string"
}
```

## Request Parameters<a name="API_DescribeAgent_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgentArn](#API_DescribeAgent_RequestSyntax) **   <a name="DataSync-DescribeAgent-request-AgentArn"></a>
The Amazon Resource Name \(ARN\) of the agent to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeAgent_ResponseSyntax"></a>

```
{
   "AgentArn": "string",
   "CreationTime": number,
   "EndpointType": "string",
   "LastConnectionTime": number,
   "Name": "string",
   "PrivateLinkConfig": { 
      "PrivateLinkEndpoint": "string",
      "SecurityGroupArns": [ "string" ],
      "SubnetArns": [ "string" ],
      "VpcEndpointId": "string"
   },
   "Status": "string"
}
```

## Response Elements<a name="API_DescribeAgent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AgentArn](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-AgentArn"></a>
The Amazon Resource Name \(ARN\) of the agent\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$` 

 ** [CreationTime](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-CreationTime"></a>
The time that the agent was activated \(that is, created in your account\)\.  
Type: Timestamp

 ** [EndpointType](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-EndpointType"></a>
The type of endpoint that your agent is connected to\. If the endpoint is a VPC endpoint, the agent is not accessible over the public internet\.   
Type: String  
Valid Values:` PUBLIC | PRIVATE_LINK | FIPS` 

 ** [LastConnectionTime](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-LastConnectionTime"></a>
The time that the agent last connected to DataSync\.  
Type: Timestamp

 ** [Name](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-Name"></a>
The name of the agent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$` 

 ** [PrivateLinkConfig](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-PrivateLinkConfig"></a>
The subnet and the security group that DataSync used to access a VPC endpoint\.  
Type: [PrivateLinkConfig](API_PrivateLinkConfig.md) object

 ** [Status](#API_DescribeAgent_ResponseSyntax) **   <a name="DataSync-DescribeAgent-response-Status"></a>
The status of the agent\. If the status is ONLINE, then the agent is configured properly and is available to use\. The Running status is the normal running status for an agent\. If the status is OFFLINE, the agent's VM is turned off or the agent is in an unhealthy state\. When the issue that caused the unhealthy state is resolved, the agent returns to ONLINE status\.  
Type: String  
Valid Values:` ONLINE | OFFLINE` 

## Errors<a name="API_DescribeAgent_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeAgent_Examples"></a>

### Example<a name="API_DescribeAgent_Example_1"></a>

The following example returns information about the agent specified in the sample request\.

#### Sample Request<a name="API_DescribeAgent_Example_1_Request"></a>

```
{
  "AgentArn": "arn:aws:datasync:us-east-2:111222333444:agent/agent-0b0addbeef44baca3"
}
```

### Example<a name="API_DescribeAgent_Example_2"></a>

This example illustrates one usage of DescribeAgent\.

#### Sample Response<a name="API_DescribeAgent_Example_2_Response"></a>

```
{
  "AgentArn": "arn:aws:datasync:us-east-2:111222333444:agent/agent-0b0addbeef44baca3",
  "CreationTime": "1532660733.39",
  "LastConnectionTime": "1532660733.39",
  "Name": "MyAgent",
  "Status": "ONLINE"
}
```

## See Also<a name="API_DescribeAgent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeAgent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeAgent) 