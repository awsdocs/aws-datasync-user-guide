# DescribeLocationFsxOntap<a name="API_DescribeLocationFsxOntap"></a>

Provides details about how an AWS DataSync location for an Amazon FSx for NetApp ONTAP file system is configured\.

**Note**  
If your location uses SMB, the `DescribeLocationFsxOntap` operation doesn't actually return a `Password`\.

## Request Syntax<a name="API_DescribeLocationFsxOntap_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationFsxOntap_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationFsxOntap_RequestSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-request-LocationArn"></a>
Specifies the Amazon Resource Name \(ARN\) of the FSx for ONTAP file system location that you want information about\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationFsxOntap_ResponseSyntax"></a>

```
{
   "CreationTime": number,
   "FsxFilesystemArn": "string",
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
   "SecurityGroupArns": [ "string" ],
   "StorageVirtualMachineArn": "string"
}
```

## Response Elements<a name="API_DescribeLocationFsxOntap_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-CreationTime"></a>
The time that the location was created\.  
Type: Timestamp

 ** [FsxFilesystemArn](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-FsxFilesystemArn"></a>
The ARN of the FSx for ONTAP file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):fsx:[a-z\-0-9]*:[0-9]{12}:file-system/fs-.*$` 

 ** [LocationArn](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-LocationArn"></a>
The ARN of the FSx for ONTAP file system location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-LocationUri"></a>
The uniform resource identifier \(URI\) of the FSx for ONTAP file system location\.  
Type: String  
Length Constraints: Maximum length of 4360\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9-]+)://[a-zA-Z0-9.:/\-]+$` 

 ** [Protocol](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-Protocol"></a>
Specifies the data transfer protocol that AWS DataSync uses to access your Amazon FSx file system\.  
Type: [FsxProtocol](API_FsxProtocol.md) object

 ** [SecurityGroupArns](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-SecurityGroupArns"></a>
The security groups that DataSync uses to access your FSx for ONTAP file system\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$` 

 ** [StorageVirtualMachineArn](#API_DescribeLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-DescribeLocationFsxOntap-response-StorageVirtualMachineArn"></a>
The ARN of the storage virtual machine \(SVM\) on your FSx for ONTAP file system where you're copying data to or from\.  
Type: String  
Length Constraints: Maximum length of 162\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):fsx:[a-z\-0-9]+:[0-9]{12}:storage-virtual-machine/fs-[0-9a-f]+/svm-[0-9a-f]{17,}$` 

## Errors<a name="API_DescribeLocationFsxOntap_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeLocationFsxOntap_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationFsxOntap) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationFsxOntap) 