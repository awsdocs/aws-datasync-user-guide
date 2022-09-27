# DescribeLocationFsxOpenZfs<a name="API_DescribeLocationFsxOpenZfs"></a>

Provides details about how an AWS DataSync location for an Amazon FSx for OpenZFS file system is configured\.

**Note**  
Response elements related to `SMB` aren't supported with the `DescribeLocationFsxOpenZfs` operation\.

## Request Syntax<a name="API_DescribeLocationFsxOpenZfs_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationFsxOpenZfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationFsxOpenZfs_RequestSyntax) **   <a name="DataSync-DescribeLocationFsxOpenZfs-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the FSx for OpenZFS location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationFsxOpenZfs_ResponseSyntax"></a>

```
{
   "CreationTime": number,
   "LocationArn": "string",
   "LocationUri": "string",
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
   "SecurityGroupArns": [ "string" ]
}
```

## Response Elements<a name="API_DescribeLocationFsxOpenZfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribeLocationFsxOpenZfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOpenZfs-response-CreationTime"></a>
The time that the FSx for OpenZFS location was created\.  
Type: Timestamp

 ** [LocationArn](#API_DescribeLocationFsxOpenZfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOpenZfs-response-LocationArn"></a>
The ARN of the FSx for OpenZFS location that was described\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationFsxOpenZfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOpenZfs-response-LocationUri"></a>
The uniform resource identifier \(URI\) of the FSx for OpenZFS location that was described\.  
Example: `fsxz://us-west-2.fs-1234567890abcdef02/fsx/folderA/folder`   
Type: String  
Length Constraints: Maximum length of 4360\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9-]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [Protocol](#API_DescribeLocationFsxOpenZfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOpenZfs-response-Protocol"></a>
The type of protocol that AWS DataSync uses to access your file system\.  
Type: [FsxProtocol](API_FsxProtocol.md) object

 ** [SecurityGroupArns](#API_DescribeLocationFsxOpenZfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOpenZfs-response-SecurityGroupArns"></a>
The ARNs of the security groups that are configured for the FSx for OpenZFS file system\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$` 

## Errors<a name="API_DescribeLocationFsxOpenZfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeLocationFsxOpenZfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationFsxOpenZfs) 