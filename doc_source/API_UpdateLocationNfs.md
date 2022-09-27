# UpdateLocationNfs<a name="API_UpdateLocationNfs"></a>

Updates some of the parameters of a previously created location for Network File System \(NFS\) access\. For information about creating an NFS location, see [Creating a location for NFS](https://docs.aws.amazon.com/datasync/latest/userguide/create-nfs-location.html)\.

## Request Syntax<a name="API_UpdateLocationNfs_RequestSyntax"></a>

```
{
   "LocationArn": "string",
   "MountOptions": { 
      "Version": "string"
   },
   "OnPremConfig": { 
      "AgentArns": [ "string" ]
   },
   "Subdirectory": "string"
}
```

## Request Parameters<a name="API_UpdateLocationNfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_UpdateLocationNfs_RequestSyntax) **   <a name="DataSync-UpdateLocationNfs-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the NFS location to update\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

 ** [MountOptions](#API_UpdateLocationNfs_RequestSyntax) **   <a name="DataSync-UpdateLocationNfs-request-MountOptions"></a>
Specifies how DataSync can access a location using the NFS protocol\.  
Type: [NfsMountOptions](API_NfsMountOptions.md) object  
Required: No

 ** [OnPremConfig](#API_UpdateLocationNfs_RequestSyntax) **   <a name="DataSync-UpdateLocationNfs-request-OnPremConfig"></a>
A list of Amazon Resource Names \(ARNs\) of agents to use for a Network File System \(NFS\) location\.  
Type: [OnPremConfig](API_OnPremConfig.md) object  
Required: No

 ** [Subdirectory](#API_UpdateLocationNfs_RequestSyntax) **   <a name="DataSync-UpdateLocationNfs-request-Subdirectory"></a>
The subdirectory in the NFS file system that is used to read data from the NFS source location or write data to the NFS destination\. The NFS path should be a path that's exported by the NFS server, or a subdirectory of that path\. The path should be such that it can be mounted by other NFS clients in your network\.  
To see all the paths exported by your NFS server, run "`showmount -e nfs-server-name`" from an NFS client that has access to your server\. You can specify any directory that appears in the results, and any subdirectory of that directory\. Ensure that the NFS export is accessible without Kerberos authentication\.   
To transfer all the data in the folder that you specified, DataSync must have permissions to read all the data\. To ensure this, either configure the NFS export with `no_root_squash`, or ensure that the files you want DataSync to access have permissions that allow read access for all users\. Doing either option enables the agent to read the files\. For the agent to access directories, you must additionally enable all execute access\.  
If you are copying data to or from your AWS Snowcone device, see [NFS Server on AWS Snowcone](https://docs.aws.amazon.com/datasync/latest/userguide/create-nfs-location.html#nfs-on-snowcone) for more information\.  
For information about NFS export configuration, see [18\.7\. The /etc/exports Configuration File](http://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/s1-nfs-server-config-exports.html) in the Red Hat Enterprise Linux documentation\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]+$`   
Required: No

## Response Elements<a name="API_UpdateLocationNfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateLocationNfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateLocationNfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/UpdateLocationNfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/UpdateLocationNfs) 