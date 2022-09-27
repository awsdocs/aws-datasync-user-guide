# CreateLocationEfs<a name="API_CreateLocationEfs"></a>

Creates an endpoint for an Amazon EFS file system that AWS DataSync can access for a transfer\. For more information, see [Creating a location for Amazon EFS](https://docs.aws.amazon.com/datasync/latest/userguide/create-efs-location.html)\.

## Request Syntax<a name="API_CreateLocationEfs_RequestSyntax"></a>

```
{
   "AccessPointArn": "string",
   "Ec2Config": { 
      "SecurityGroupArns": [ "string" ],
      "SubnetArn": "string"
   },
   "EfsFilesystemArn": "string",
   "FileSystemAccessRoleArn": "string",
   "InTransitEncryption": "string",
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

 ** [AccessPointArn](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-AccessPointArn"></a>
Specifies the Amazon Resource Name \(ARN\) of the access point that DataSync uses to access the Amazon EFS file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):elasticfilesystem:[a-z\-0-9]+:[0-9]{12}:access-point/fsap-[0-9a-f]{8,40}$`   
Required: No

 ** [Ec2Config](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-Ec2Config"></a>
Specifies the subnet and security groups DataSync uses to access your Amazon EFS file system\.  
Type: [Ec2Config](API_Ec2Config.md) object  
Required: Yes

 ** [EfsFilesystemArn](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-EfsFilesystemArn"></a>
Specifies the ARN for the Amazon EFS file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):elasticfilesystem:[a-z\-0-9]*:[0-9]{12}:file-system/fs-.*$`   
Required: Yes

 ** [FileSystemAccessRoleArn](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-FileSystemAccessRoleArn"></a>
Specifies an AWS Identity and Access Management \(IAM\) role that DataSync assumes when mounting the Amazon EFS file system\.  
Type: String  
Length Constraints: Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):iam::[0-9]{12}:role/.*$`   
Required: No

 ** [InTransitEncryption](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-InTransitEncryption"></a>
Specifies whether you want DataSync to use Transport Layer Security \(TLS\) 1\.2 encryption when it copies data to or from the Amazon EFS file system\.  
If you specify an access point using `AccessPointArn` or an IAM role using `FileSystemAccessRoleArn`, you must set this parameter to `TLS1_2`\.  
Type: String  
Valid Values:` NONE | TLS1_2`   
Required: No

 ** [Subdirectory](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-Subdirectory"></a>
Specifies a mount path for your Amazon EFS file system\. This is where DataSync reads or writes data \(depending on if this is a source or destination location\)\. By default, DataSync uses the root directory, but you can also include subdirectories\.  
You must specify a value with forward slashes \(for example, `/path/to/folder`\)\.
Type: String  
Length Constraints: Maximum length of 4096\.  
Pattern: `^[a-zA-Z0-9_\-\+\./\(\)\p{Zs}]*$`   
Required: No

 ** [Tags](#API_CreateLocationEfs_RequestSyntax) **   <a name="DataSync-CreateLocationEfs-request-Tags"></a>
Specifies the key\-value pair that represents a tag that you want to add to the resource\. The value can be an empty string\. This value helps you manage, filter, and search for your resources\. We recommend that you create a name tag for your location\.  
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
The Amazon Resource Name \(ARN\) of the Amazon EFS file system location that you create\.  
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

### Sample Request<a name="API_CreateLocationEfs_Example_1"></a>

The following example creates a location for an Amazon EFS file system\.

#### <a name="w326aac37b7c14c15b3b5"></a>

```
{
    "Ec2Config": {
        "SubnetArn": "arn:aws:ec2:us-east-2:11122233344:subnet/subnet-1234567890abcdef1",
        "SecurityGroupArns": [
            "arn:aws:ec2:us-east-2:11122233344:security-group/sg-1234567890abcdef2"
        ]
    },
    "EfsFilesystemArn": "arn:aws:elasticfilesystem:us-east-2:111222333444:file-system/fs-021345abcdef6789",
    "Subdirectory": "/mount/path",
    "Tags": [{
        "Key": "Name",
        "Value": "ElasticFileSystem-1"
    }]
}
```

### Sample Request: Creating a location for a restricted Amazon EFS file system<a name="API_CreateLocationEfs_Example_2"></a>

The following example creates a location for an Amazon EFS file system with restricted access\. In this kind of scenario, you might have to specify values for `AccessPointArn`, `FileSystemAccessRoleArn`, and `InTransitEncryption` in your request\.

#### <a name="w326aac37b7c14c15b5b5"></a>

```
{
    "AccessPointArn": "arn:aws:elasticfilesystem:us-east-2:111222333444:access-point/fsap-1234567890abcdef0",
    "Ec2Config": {
        "SubnetArn": "arn:aws:ec2:us-east-2:111222333444:subnet/subnet-1234567890abcdef1",
        "SecurityGroupArns": [
            "arn:aws:ec2:us-east-2:111222333444:security-group/sg-1234567890abcdef2"
        ]
    },
    "FileSystemAccessRoleArn": "arn:aws:iam::111222333444:role/AwsDataSyncFullAccessNew",
    "InTransitEncryption": "TLS1_2",
    "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-abcdef01234567890",
    "LocationUri": "efs://us-east-2.fs-021345abcdef6789/",
    "Subdirectory": "/mount/path",
    "Tags": [{
        "Key": "Name",
        "Value": "ElasticFileSystem-1"
    }]
}
```

### Sample Response<a name="API_CreateLocationEfs_Example_3"></a>

A response returns the location ARN of the Amazon EFS file system\.

#### <a name="w326aac37b7c14c15b7b5"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-12abcdef012345678"
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