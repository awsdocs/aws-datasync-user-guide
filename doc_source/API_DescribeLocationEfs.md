# DescribeLocationEfs<a name="API_DescribeLocationEfs"></a>

Returns metadata, such as the path information about an Amazon EFS location\.

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
The Amazon Resource Name \(ARN\) of the EFS location to describe\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: Yes

## Response Syntax<a name="API_DescribeLocationEfs_ResponseSyntax"></a>

```
{
   "CreationTime": number,
   "Ec2Config": { 
      "SecurityGroupArns": [ "string" ],
      "SubnetArn": "string"
   },
   "LocationArn": "string",
   "LocationUri": "string"
}
```

## Response Elements<a name="API_DescribeLocationEfs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTime](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-CreationTime"></a>
The time that the EFS location was created\.  
Type: Timestamp

 ** [Ec2Config](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-Ec2Config"></a>
The subnet that AWS DataSync uses to access target EFS file system\. The subnet must have at least one mount target for that file system\. The security group that you provide needs to be able to communicate with the security group on the mount target in the subnet specified\.   
Type: [Ec2Config](API_Ec2Config.md) object

 ** [LocationArn](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the EFS location that was described\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$` 

 ** [LocationUri](#API_DescribeLocationEfs_ResponseSyntax) **   <a name="DataSync-DescribeLocationEfs-response-LocationUri"></a>
The URL of the EFS location that was described\.  
Type: String  
Length Constraints: Maximum length of 4356\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9]+)://[a-zA-Z0-9.:/\-]+$` 

## Errors<a name="API_DescribeLocationEfs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** InternalException **   
This exception is thrown when an error occurs in the AWS DataSync service\.  
HTTP Status Code: 500

 ** InvalidRequestException **   
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## Examples<a name="API_DescribeLocationEfs_Examples"></a>

### Example<a name="API_DescribeLocationEfs_Example_1"></a>

The following example returns information about the Amazon EFS location specified in the sample request\.

#### Sample Request<a name="API_DescribeLocationEfs_Example_1_Request"></a>

```
{
  "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50fb"
}
```

### Example<a name="API_DescribeLocationEfs_Example_2"></a>

This example illustrates one usage of DescribeLocationEfs\.

#### Sample Response<a name="API_DescribeLocationEfs_Example_2_Response"></a>

```
{
    "CreationTime": "",
    "Ec2Config": {
        "SecurityGroupArns": [
            "arn:aws:ec2:us-east-2:11122233344:security-group/sg-0117195988293d62f"
        ],
        "SubnetArn": "arn:aws:ec2:us-east-2:11122233344:subnet/subnet-f45a0e678"
    },
    "LocationArn": "arn:aws:datasync:us-east-2:111222333444:location/loc-07db7abfc326c50fb",
    "LocationUri": "efs://us-east-2.fs-abcd1234. "
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