# DescribeLocationEfs<a name="API_DescribeLocationEfs"></a>

Returns metadata about your AWS DataSync location for an Amazon EFS file system\.

## Request Syntax<a name="API_DescribeLocationEfs_RequestSyntax"></a>

```
{
   "LocationArn": "string"
}
```

## Request Parameters<a name="API_DescribeLocationEfs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LocationArn](#API_DescribeLocationEfs_RequestSyntax) **   <a name="DataSync-DescribeLocationEfs-request-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon EFS file system location that you want information about\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationEfs_ResponseSyntax"></a>

```
{
   "AccessPointArn": "string",
   "CreationTime": number,
   "Ec2Config": { 
      "SecurityGroupArns": [ "string" ],
      "SubnetArn": "string"
   },
   "FileSystemAccessRoleArn": "string",
   "InTransitEncryption": "string",
   "LocationArn": "string",
   "LocationUri": "string"
}
```

## Response Elements<a name="API_DescribeLocationEfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AccessPointArn](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-AccessPointArn"></a>
The ARN of the access point that DataSync uses to access the Amazon EFS file system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):elasticfilesystem:[a-z\-0-9]+:[0-9]{12}:access-point/fsap-[0-9a-f]{8,40}$` 

 ** [CreationTime](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-CreationTime"></a>
The time that the location was created\.  
Type: Timestamp

 ** [Ec2Config](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-Ec2Config"></a>
The subnet and security groups that AWS DataSync uses to access your Amazon EFS file system\.  
Type: [Ec2Config](API_Ec2Config.md) object

 ** [FileSystemAccessRoleArn](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-FileSystemAccessRoleArn"></a>
The AWS Identity and Access Management \(IAM\) role that DataSync assumes when mounting the Amazon EFS file system\.  
Type: String  
Length Constraints: Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):iam::[0-9]{12}:role/.*$` 

 ** [InTransitEncryption](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-InTransitEncryption"></a>
Describes whether DataSync uses Transport Layer Security \(TLS\) encryption when copying data to or from the Amazon EFS file system\.  
Type: String  
Valid Values:` NONE | TLS1_2` 

 ** [LocationArn](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-LocationArn"></a>
The ARN of the Amazon EFS file system location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-LocationUri"></a>
The URL of the Amazon EFS file system location\.  
Type: String  
Length Constraints: Maximum length of 4360\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9-]+)://[a-zA-Z0-9.:/\-]+$` 

## Errors<a name="API_DescribeLocationEfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeLocationEfs_Examples"></a>

### Sample Request<a name="API_DescribeLocationEfs_Example_1"></a>

The following example shows how to get information about a specific Amazon EFS file system location\.

#### <a name="w326aac37b7c59c15b3b5"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-12abcdef012345678"
}
```

### Sample Response<a name="API_DescribeLocationEfs_Example_2"></a>

The following example returns location details about an Amazon EFS file system\.

#### <a name="w326aac37b7c59c15b5b5"></a>

```
{
    "CreationTime": 1653319021.353,
    "Ec2Config": {
        "SubnetArn": "arn:aws:ec2:us-east-2:111222333444:subnet/subnet-1234567890abcdef1",
        "SecurityGroupArns": [
            "arn:aws:ec2:us-east-2:111222333444:security-group/sg-1234567890abcdef2"
        ]
    },
    "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-abcdef01234567890",
    "LocationUri": "efs://us-east-2.fs-021345abcdef6789/"
}
```

### Sample Response: Describing a location for a restricted Amazon EFS file system<a name="API_DescribeLocationEfs_Example_3"></a>

The following example returns location details about an Amazon EFS file system with restricted access, including the `AccessPointArn`, `FileSystemAccessRoleArn`, and `InTransitEncryption` elements\.

#### <a name="w326aac37b7c59c15b7b5"></a>

```
{
    "CreationTime": 1653319021.353,
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

## See Also<a name="API_DescribeLocationEfs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/datasync-2018-11-09/DescribeLocationEfs) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/DescribeLocationEfs) 