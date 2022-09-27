# UpdateLocationSmb<a name="API_UpdateLocationSmb"></a>

Updates some of the parameters of a previously created location for Server Message Block \(SMB\) file system access\. For information about creating an SMB location, see [Creating a location for SMB](https://docs.aws.amazon.com/datasync/latest/userguide/create-smb-location.html)\.

## Request Syntax<a name="API_UpdateLocationSmb_RequestSyntax"></a>

```
{
   "AgentArns": [ "string" ],
   "Domain": "string",
   "LocationArn": "string",
   "MountOptions": { 
      "Version": "string"
   },
   "Password": "string",
   "Subdirectory": "string",
   "User": "string"
}
```

## Request Parameters<a name="API_UpdateLocationSmb_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AgentArns](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-AgentArns"></a>
The Amazon Resource Names \(ARNs\) of agents to use for a Simple Message Block \(SMB\) location\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`   
Required: No

 ** [Domain](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-Domain"></a>
The name of the Windows domain that the SMB server belongs to\.  
Type: String  
Length Constraints: Maximum length of 253\.  
Pattern: `^[A-Za-z0-9]((\.|-+)?[A-Za-z0-9]){0,252}$`   
Required: No

 ** [LocationArn](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the SMB location to update\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

 ** [MountOptions](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-MountOptions"></a>
Specifies how DataSync can access a location using the SMB protocol\.  
Type: [SmbMountOptions](API_SmbMountOptions.md) object  
Required: No

 ** [Password](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-Password"></a>
The password of the user who can mount the share has the permissions to access files and folders in the SMB share\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^.{0,104}$`   
Required: No

 ** [Subdirectory](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-Subdirectory"></a>
The subdirectory in the SMB file system that is used to read data from the SMB source location or write data to the SMB destination\. The SMB path should be a path that's exported by the SMB server, or a subdirectory of that path\. The path should be such that it can be mounted by other SMB clients in your network\.  
 `Subdirectory` must be specified with forward slashes\. For example, `/path/to/folder`\.
To transfer all the data in the folder that you specified, DataSync must have permissions to mount the SMB share and to access all the data in that share\. To ensure this, do either of the following:  
+ Ensure that the user/password specified belongs to the user who can mount the share and who has the appropriate permissions for all of the files and directories that you want DataSync to access\.
+ Use credentials of a member of the Backup Operators group to mount the share\. 
Doing either of these options enables the agent to access the data\. For the agent to access directories, you must also enable all execute access\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\$\p{Zs}]+$`   
Required: No

 ** [User](#API_UpdateLocationSmb_RequestSyntax) **   <a name="DataSync-UpdateLocationSmb-request-User"></a>
The user who can mount the share has the permissions to access files and folders in the SMB share\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^[^\x5B\x5D\\/:;|=,+*?]{1,104}$`   
Required: No

## Response Elements<a name="API_UpdateLocationSmb_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateLocationSmb_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateLocationSmb_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/UpdateLocationSmb) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/UpdateLocationSmb) 