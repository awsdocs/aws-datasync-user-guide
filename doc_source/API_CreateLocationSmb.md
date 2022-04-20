# CreateLocationSmb<a name="API_CreateLocationSmb"></a>

Defines a file system on a Server Message Block \(SMB\) server that can be read from or written to\.

## Request Syntax<a name="API_CreateLocationSmb_RequestSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "Domain": "string",
   "MountOptions": { 
      "Version": "string"
   },
   "Password": "string",
   "ServerHostname": "string",
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "User": "string"
}
```

## Request Parameters<a name="API_CreateLocationSmb_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgentArns](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-AgentArns"></a>
The Amazon Resource Names \(ARNs\) of agents to use for a Simple Message Block \(SMB\) location\.   
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: Yes

 ** [Domain](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-Domain"></a>
The name of the Windows domain that the SMB server belongs to\.  
Type: String  
Length Constraints: Maximum length of 253\.  
Pattern: `^([A-Za-z0-9]+[A-Za-z0-9-.]*)*[A-Za-z0-9-]*[A-Za-z0-9]$`   
Required: No

 ** [MountOptions](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-MountOptions"></a>
The mount options used by DataSync to access the SMB server\.  
Type: [SmbMountOptions](API_SmbMountOptions.md) object  
Required: No

 ** [Password](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-Password"></a>
The password of the user who can mount the share, has the permissions to access files and folders in the SMB share\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^.{0,104}$`   
Required: Yes

 ** [ServerHostname](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-ServerHostname"></a>
The name of the SMB server\. This value is the IP address or Domain Name Service \(DNS\) name of the SMB server\. An agent that is installed on\-premises uses this hostname to mount the SMB server in a network\.  
This name must either be DNS\-compliant or must be an IP version 4 \(IPv4\) address\.
Type: String  
Length Constraints: Maximum length of 255\.  
Pattern: `^(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-Subdirectory"></a>
The subdirectory in the SMB file system that is used to read data from the SMB source location or write data to the SMB destination\. The SMB path should be a path that's exported by the SMB server, or a subdirectory of that path\. The path should be such that it can be mounted by other SMB clients in your network\.  
 `Subdirectory` must be specified with forward slashes\. For example, `/path/to/folder`\.
To transfer all the data in the folder you specified, DataSync needs to have permissions to mount the SMB share, as well as to access all the data in that share\. To ensure this, either ensure that the user/password specified belongs to the user who can mount the share, and who has the appropriate permissions for all of the files and directories that you want DataSync to access, or use credentials of a member of the Backup Operators group to mount the share\. Doing either enables the agent to access the data\. For the agent to access directories, you must additionally enable all execute access\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: Yes

 ** [Tags](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-Tags"></a>
The key\-value pair that represents the tag that you want to add to the location\. The value can be an empty string\. We recommend using tags to name your resources\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

 ** [User](#API_CreateLocationSmb_RequestSyntax) **   <a name="DataSync-CreateLocationSmb-request-User"></a>
The user who can mount the share, has the permissions to access files and folders in the SMB share\.  
For information about choosing a user name that ensures sufficient permissions to files, folders, and metadata, see [user](create-smb-location.html#SMBuser)\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^[^\x5B\x5D\\/:;|=,+*?]{1,104}$`   
Required: Yes

## Response Syntax<a name="API_CreateLocationSmb_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationSmb_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationSmb_ResponseSyntax) **   <a name="DataSync-CreateLocationSmb-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the source SMB file system location that is created\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationSmb_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_CreateLocationSmb_Examples"></a>

### Example<a name="API_CreateLocationSmb_Example_1"></a>

This example illustrates one usage of CreateLocationSmb\.

#### Sample Request<a name="API_CreateLocationSmb_Example_1_Request"></a>

```
{
   "AgentArns":[
      "arn:aws:datasync:us-east-2:111222333444:agent/agent-0b0addbeef44b3nfs",
      "arn:aws:datasync:us-east-2:111222333444:agent/agent-2345noo35nnee1123ovo3"
   ],
   "Domain":"AMAZON",
   "MountOptions":{
      "Version":"SMB3"
   },
   "Password":"string",
   "ServerHostname":"MyServer.amazon.com",
   "Subdirectory":"share",
   "Tags":[
      {
         "Key":"department",
         "Value":"finance"
      }
   ],
   "User":"user-1"
}
```

### Example<a name="API_CreateLocationSmb_Example_2"></a>

This example illustrates one usage of CreateLocationSmb\.

#### Sample Response<a name="API_CreateLocationSmb_Example_2_Response"></a>

```
{"arn:aws:datasync:us-east-1:111222333444:location/loc-0f01451b140b2af49"}
```

## See Also<a name="API_CreateLocationSmb_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationSmb) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationSmb) 