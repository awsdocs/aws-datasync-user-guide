# CreateLocationFsxOpenZfs<a name="API_CreateLocationFsxOpenZfs"></a>

Creates an endpoint for an Amazon FSx for OpenZFS file system that AWS DataSync can access for a transfer\. For more information, see [Creating a location for FSx for OpenZFS](https://docs.aws.amazon.com/datasync/latest/userguide/create-openzfs-location.html)\.

**Note**  
Request parameters related to `SMB` aren't supported with the `CreateLocationFsxOpenZfs` operation\.

## Request Syntax<a name="API_CreateLocationFsxOpenZfs_RequestSyntax"></a>

```
{
   "FsxFilesystemArn": "string",
   "Protocol": { 
      "NFS": { 
         "MountOptions": { 
            "Version": "string"
         }
      },
      "SMB": { 
         "Domain": "string",
         "MountOptions": { 
            "Version": "string"
         },
         "Password": "string",
         "User": "string"
      }
   },
   "SecurityGroupArns": [ "string" ],
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationFsxOpenZfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [FsxFilesystemArn](#API_CreateLocationFsxOpenZfs_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOpenZfs-request-FsxFilesystemArn"></a>
The Amazon Resource Name \(ARN\) of the FSx for OpenZFS file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):fsx:[a-z\-0-9]*:[0-9]{12}:file-system/fs-.*$`   
Required: Yes

 ** [Protocol](#API_CreateLocationFsxOpenZfs_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOpenZfs-request-Protocol"></a>
The type of protocol that AWS DataSync uses to access your file system\.  
Type: [FsxProtocol](API_FsxProtocol.md) object  
Required: Yes

 ** [SecurityGroupArns](#API_CreateLocationFsxOpenZfs_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOpenZfs-request-SecurityGroupArns"></a>
The ARNs of the security groups that are used to configure the FSx for OpenZFS file system\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationFsxOpenZfs_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOpenZfs-request-Subdirectory"></a>
A subdirectory in the location's path that must begin with `/fsx`\. DataSync uses this subdirectory to read or write data \(depending on whether the file system is a source or destination location\)\.  
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[^\u0000\u0085\u2028\u2029\r\n]{1,4096}$`   
Required: No

 ** [Tags](#API_CreateLocationFsxOpenZfs_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOpenZfs-request-Tags"></a>
The key\-value pair that represents a tag that you want to add to the resource\. The value can be an empty string\. This value helps you manage, filter, and search for your resources\. We recommend that you create a name tag for your location\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationFsxOpenZfs_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationFsxOpenZfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationFsxOpenZfs_ResponseSyntax) **   <a name="DataSync-CreateLocationFsxOpenZfs-response-LocationArn"></a>
The ARN of the FSx for OpenZFS file system location that you created\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationFsxOpenZfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateLocationFsxOpenZfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationFsxOpenZfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationFsxOpenZfs) 