# CreateLocationEfs<a name="API_CreateLocationEfs"></a>

Creates an endpoint for an Amazon EFS file system\.

## Request Syntax<a name="API_CreateLocationEfs_RequestSyntax"></a>

```
{
   "Ec2Config": { 
      "SecurityGroupArns": [ "string" ],
      "SubnetArn": "string"
   },
   "EfsFilesystemArn": "string",
   "Subdirectory": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateLocationEfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Ec2Config](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-Ec2Config"></a>
The subnet and security group that the Amazon EFS file system uses\. The security group that you provide needs to be able to communicate with the security group on the mount target in the subnet specified\.  
The exact relationship between security group M \(of the mount target\) and security group S \(which you provide for DataSync to use at this stage\) is as follows:   
+  Security group M \(which you associate with the mount target\) must allow inbound access for the Transmission Control Protocol \(TCP\) on the NFS port \(2049\) from security group S\. You can enable inbound connections either by IP address \(CIDR range\) or security group\. 
+ Security group S \(provided to DataSync to access EFS\) should have a rule that enables outbound connections to the NFS port on one of the file system’s mount targets\. You can enable outbound connections either by IP address \(CIDR range\) or security group\.

  For information about security groups and mount targets, see [Security Groups for Amazon EC2 Instances and Mount Targets](https://docs.aws.amazon.com/efs/latest/ug/security-considerations.html#network-access) in the *Amazon EFS User Guide\.* 
Type: [Ec2Config](API_Ec2Config.md) object  
Required: Yes

 ** [EfsFilesystemArn](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-EfsFilesystemArn"></a>
The Amazon Resource Name \(ARN\) for the Amazon EFS file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):elasticfilesystem:[a-z\-0-9]*:[0-9]{12}:file-system/fs-.*$`   
Required: Yes

 ** [Subdirectory](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-Subdirectory"></a>
A subdirectory in the location’s path\. This subdirectory in the EFS file system is used to read data from the EFS source location or write data to the EFS destination\. By default, AWS DataSync uses the root directory\.  
 `Subdirectory` must be specified with forward slashes\. For example, `/path/to/folder`\.
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]*$`   
Required: No

 ** [Tags](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-Tags"></a>
The key\-value pair that represents a tag that you want to add to the resource\. The value can be an empty string\. This value helps you manage, filter, and search for your resources\. We recommend that you create a name tag for your location\.  
Type: Array of [TagListEntry](API_TagListEntry.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

## Response Syntax<a name="API_CreateLocationEfs_ResponseSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Response Elements<a name="API_CreateLocationEfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LocationArn](#API_CreateLocationEfs_ResponseSyntax) **   <a name="DataSync-CreateLocationEfs-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon EFS file system location that is created\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

## Errors<a name="API_CreateLocationEfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_CreateLocationEfs_Examples"></a>

### Example<a name="API_CreateLocationEfs_Example_1"></a>

The following example creates an endpoint for an Amazon EFS file system\.

#### Sample Request<a name="API_CreateLocationEfs_Example_1_Request"></a>

```
{
  "Ec2Config": {
     SecurityGroupArns": ["arn:aws:ec2:us-east-2:11122233344:security-group/sg-0117195988293d62f"],
     "SubnetArn": "arn:aws:ec2:us-east-2:11122233344:subnet/subnet-f45a0e678",
  },
  "EfsFilesystemArn" :"arn:aws:elasticfilesystem:us-east-2:111222333444:file-system/fs-12345efs",
  "Subdirectory": "/MySubdirectory",
  "Tags": [
        {
           "Key": "Name",
           "Value": "ElasticFileSystem-1"
        }
      ]
}
```

### Example<a name="API_CreateLocationEfs_Example_2"></a>

The response returns the Amazon Resource Name \(ARN\) of the EFS location\.

#### Sample Response<a name="API_CreateLocationEfs_Example_2_Response"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50fb"
}
```

## See Also<a name="API_CreateLocationEfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/CreateLocationEfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/CreateLocationEfs) 