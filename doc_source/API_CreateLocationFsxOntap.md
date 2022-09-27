# CreateLocationFsxOntap<a name="API_CreateLocationFsxOntap"></a>

Creates an endpoint for an Amazon FSx for NetApp ONTAP file system that AWS DataSync can access for a transfer\. For more information, see [Creating a location for FSx for ONTAP](https://docs.aws.amazon.com/datasync/latest/userguide/create-ontap-location.html)\.

## Request Syntax<a name="API_CreateLocationFsxOntap_RequestSyntax"></a>

```
{
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
   "StorageVirtualMachineArn": "string",
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationFsxOntap_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Protocol](#API_CreateLocationFsxOntap_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOntap-request-Protocol"></a>
Specifies the data transfer protocol that AWS DataSync uses to access your Amazon FSx file system\.  
Type: [FsxProtocol](API_FsxProtocol.md) object  
Required: Yes

 ** [SecurityGroupArns](#API_CreateLocationFsxOntap_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOntap-request-SecurityGroupArns"></a>
Specifies the Amazon EC2 security groups that provide access to your file system's preferred subnet\.  
The security groups must allow outbound traffic on the following ports \(depending on the protocol you use\):  
+  **Network File System \(NFS\)**: TCP ports 111, 635, and 2049
+  **Server Message Block \(SMB\)**: TCP port 445
Your file system's security groups must also allow inbound traffic on the same ports\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):ec2:[a-z\-0-9]*:[0-9]{12}:security-group/.*$`   
Required: Yes

 ** [StorageVirtualMachineArn](#API_CreateLocationFsxOntap_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOntap-request-StorageVirtualMachineArn"></a>
Specifies the ARN of the storage virtual machine \(SVM\) on your file system where you're copying data to or from\.  
Type: String  
Length Constraints: Maximum length of 162\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):fsx:[a-z\-0-9]+:[0-9]{12}:storage-virtual-machine/fs-[0-9a-f]+/svm-[0-9a-f]{17,}$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationFsxOntap_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOntap-request-Subdirectory"></a>
Specifies the junction path \(also known as a mount point\) in the SVM volume where you're copying data to or from \(for example, `/vol1`\)\.  
Don't specify a junction path in the SVM's root volume\. For more information, see [Managing FSx for ONTAP storage virtual machines](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/managing-svms.html) in the *Amazon FSx for NetApp ONTAP User Guide*\.
Type: String  
Length Constraints: Maximum length of 255\.  
Pattern: `^[^\u0000\u0085\u2028\u2029\r\n]{1,255}$`   
Required: No

 ** [Tags](#API_CreateLocationFsxOntap_RequestSyntax) **   <a name="DataSync-CreateLocationFsxOntap-request-Tags"></a>
Specifies labels that help you categorize, filter, and search for your AWS resources\. We recommend creating at least a name tag for your location\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationFsxOntap_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationFsxOntap_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationFsxOntap_ResponseSyntax) **   <a name="DataSync-CreateLocationFsxOntap-response-LocationArn"></a>
Specifies the ARN of the FSx for ONTAP file system location that you create\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationFsxOntap_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateLocationFsxOntap_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationFsxOntap) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationFsxOntap) 