# CreateLocationNfs<a name="API_CreateLocationNfs"></a>

Defines a file system on a Network File System \(NFS\) server that can be read from or written to\.

## Request Syntax<a name="API_CreateLocationNfs_RequestSyntax"></a>

```
{
   "MountOptions": { 
      "Version": "string"
   },
   "OnPremConfig": { 
      "AgentArns": [ "string" ]
   },
   "ServerHostname": "string",
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationNfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MountOptions](#API_CreateLocationNfs_RequestSyntax) **   <a name="DataSync-CreateLocationNfs-request-MountOptions"></a>
The NFS mount options that DataSync can use to mount your NFS share\.  
Type: [NfsMountOptions](API_NfsMountOptions.md) object  
Required: No

 ** [OnPremConfig](#API_CreateLocationNfs_RequestSyntax) **   <a name="DataSync-CreateLocationNfs-request-OnPremConfig"></a>
Contains a list of Amazon Resource Names \(ARNs\) of agents that are used to connect to an NFS server\.   
If you are copying data to or from your AWS Snowcone device, see [NFS Server on AWS Snowcone](https://docs.aws.amazon.com/datasync/latest/userguide/create-nfs-location.html#nfs-on-snowcone) for more information\.  
Type: [OnPremConfig](API_OnPremConfig.md) object  
Required: Yes

 ** [ServerHostname](#API_CreateLocationNfs_RequestSyntax) **   <a name="DataSync-CreateLocationNfs-request-ServerHostname"></a>
The name of the NFS server\. This value is the IP address or Domain Name Service \(DNS\) name of the NFS server\. An agent that is installed on\-premises uses this hostname to mount the NFS server in a network\.   
If you are copying data to or from your AWS Snowcone device, see [NFS Server on AWS Snowcone](https://docs.aws.amazon.com/datasync/latest/userguide/create-nfs-location.html#nfs-on-snowcone) for more information\.  
This name must either be DNS\-compliant or must be an IP version 4 \(IPv4\) address\.
Type: String  
Length Constraints: Maximum length of 255\.  
Pattern: `^(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationNfs_RequestSyntax) **   <a name="DataSync-CreateLocationNfs-request-Subdirectory"></a>
The subdirectory in the NFS file system that is used to read data from the NFS source location or write data to the NFS destination\. The NFS path should be a path that's exported by the NFS server, or a subdirectory of that path\. The path should be such that it can be mounted by other NFS clients in your network\.   
To see all the paths exported by your NFS server, run "`showmount -e nfs-server-name`" from an NFS client that has access to your server\. You can specify any directory that appears in the results, and any subdirectory of that directory\. Ensure that the NFS export is accessible without Kerberos authentication\.   
To transfer all the data in the folder you specified, DataSync needs to have permissions to read all the data\. To ensure this, either configure the NFS export with `no_root_squash,` or ensure that the permissions for all of the files that you want DataSync allow read access for all users\. Doing either enables the agent to read the files\. For the agent to access directories, you must additionally enable all execute access\.  
If you are copying data to or from your AWS Snowcone device, see [NFS Server on AWS Snowcone](https://docs.aws.amazon.com/datasync/latest/userguide/create-nfs-location.html#nfs-on-snowcone) for more information\.  
For information about NFS export configuration, see [18\.7\. The /etc/exports Configuration File](http://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/s1-nfs-server-config-exports.html) in the Red Hat Enterprise Linux documentation\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]+$`   
Required: Yes

 ** [Tags](#API_CreateLocationNfs_RequestSyntax) **   <a name="DataSync-CreateLocationNfs-request-Tags"></a>
The key\-value pair that represents the tag that you want to add to the location\. The value can be an empty string\. We recommend using tags to name your resources\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationNfs_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationNfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationNfs_ResponseSyntax) **   <a name="DataSync-CreateLocationNfs-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the source NFS file system location that is created\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationNfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_CreateLocationNfs_Examples"></a>

### Example<a name="API_CreateLocationNfs_Example_1"></a>

The following example creates an endpoint for an NFS file system using the specified NFS version as a mount option\.

#### Sample Request<a name="API_CreateLocationNfs_Example_1_Request"></a>

```
{
  "MountOptions": {
     "Version": : "NFS4_0"
     },
  "OnPremConfig": {
    "AgentArn": [ "arn:aws:datasync:us-east-2:111222333444:agent/agent-0b0addbeef44b3nfs" ]
          },
          
           "ServerHostname": "MyServer@amazon.com",
           "Subdirectory": "/MyFolder",
           "Tags": [
              {
                "Key": "Name",
                "Value": "ElasticFileSystem-1"
              }
           ]
}
```

### Example<a name="API_CreateLocationNfs_Example_2"></a>

The response returns the Amazon Resource Name \(ARN\) of the NFS location\.

#### Sample Response<a name="API_CreateLocationNfs_Example_2_Response"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50aa"
}
```

## See Also<a name="API_CreateLocationNfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationNfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationNfs) 