# Creating an Amazon S3 location<a name="create-s3-location"></a>

An AWS DataSync *location* is an endpoint for an Amazon S3 bucket\. You can use the location as a source or destination when copying data\.

Before you create your location, make sure that you understand what DataSync needs to access your bucket, how Amazon S3 storage classes work, and other considerations unique to Amazon S3 transfers\.

## Accessing S3 buckets<a name="create-s3-location-access"></a>

DataSync requires access to your Amazon S3 bucket\. To do this, DataSync assumes an AWS Identity and Access Management \(IAM\) role with an IAM policy and AWS Security Token Service \(AWS STS\) trust relationship\. The policy determines which actions that the role can perform\.

DataSync can create this role for you, but there are situations where you may need to create a role manually\. For more information, see [Using IAM policies to access your S3 bucket](#create-s3-location-iam)\.

## Storage class considerations with Amazon S3 locations<a name="using-storage-classes"></a>

DataSync can transfer objects directly into the [Amazon S3 storage class](http://aws.amazon.com/s3/storage-classes/) that you specify when creating your Amazon S3 location\. Some storage classes have behaviors that can affect your Amazon S3 storage costs\. For more information, see [Amazon S3 pricing](http://aws.amazon.com/s3/pricing/)\.

**Important**  
New objects copied to an S3 bucket are stored using the storage class that you specify when creating your Amazon S3 location\. DataSync won't change the storage class of existing objects in the bucket \(even if that object was modified in the source location\)\.


| Amazon S3 storage class | Considerations | 
| --- | --- | 
| S3 Standard | Choose S3 Standard to store your frequently accessed files redundantly in multiple Availability Zones that are geographically separated\. This is the default if you don't specify a storage class\.  | 
| S3 Intelligent\-Tiering |  Choose S3 Intelligent\-Tiering to optimize storage costs by automatically moving data to the most cost\-effective storage access tier\. You pay a monthly charge per object stored in the S3 Intelligent\-Tiering storage class\. This Amazon S3 charge includes monitoring data access patterns and moving objects between tiers\.  | 
| S3 Standard\-IA |  Choose S3 Standard\-IA to store your infrequently accessed files redundantly in multiple Availability Zones that are geographically separated\.  Objects stored in the S3 Standard\-IA storage class can incur additional charges for overwriting, deleting, or retrieving\. Consider how often these objects change, how long you plan to keep these objects, and how often you need to access them\. Changes to object data or metadata are equivalent to deleting an object and creating a new one to replace it\. This results in additional charges for objects stored in the S3 Standard\-IA storage class\. Objects less than 128 KB are smaller than the minimum capacity charge per object in the S3 Standard\-IA storage class\. These objects are stored in the S3 Standard storage class\.  | 
| S3 One Zone\-IA  |  Choose S3 One Zone\-IA to store your infrequently accessed files in a single Availability Zone\.  Objects stored in the S3 One Zone\-IA storage class can incur additional charges for overwriting, deleting, or retrieving\. Consider how often these objects change, how long you plan to keep these objects, and how often you need to access them\. Changes to object data or metadata are equivalent to deleting an object and creating a new one to replace it\. This results in additional charges for objects stored in the S3 One Zone\-IA storage class\. Objects less than 128 KB are smaller than the minimum capacity charge per object in the S3 One Zone\-IA storage class\. These objects are stored in the S3 Standard storage class\.  | 
| S3 Glacier Flexible Retrieval | Choose S3 Glacier Flexible Retrieval for more active archives\.Objects stored in S3 Glacier Flexible Retrieval can incur additional charges for overwriting, deleting, or retrieving\. Consider how often these objects change, how long you plan to keep these objects, and how often you need to access them\. Changes to object data or metadata are equivalent to deleting an object and creating a new one to replace it\. This results in additional charges for objects stored in the S3 Glacier Flexible Retrieval storage class\.Objects less than 40 KB are smaller than the minimum capacity charge per object in the S3 Glacier Flexible Retrieval storage class\. These objects are stored in the S3 Standard storage class\.You must restore objects archived in this storage class before DataSync can read them\. For information, see [Working with archived objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/archived-objects.html) in the Amazon S3 User Guide\.When using S3 Glacier Flexible Retrieval, choose **Verify only the data transferred** to compare data and metadata checksums at the end of the transfer\. You can't use the **Verify all data in the destination** option for this storage class because it requires retrieving all existing objects from the destination\. | 
| S3 Glacier Deep Archive |  Choose S3 Glacier Deep Archive to archive your files for long\-term data retention and digital preservation where data is accessed once or twice a year\. Objects stored in S3 Glacier Deep Archive can incur additional charges for overwriting, deleting, or retrieving\. Consider how often these objects change, how long you plan to keep these objects, and how often you need to access them\. Changes to object data or metadata are equivalent to deleting an object and creating a new one to replace it\. This results in additional charges for objects stored in the S3 Glacier Deep Archive storage class\. Objects less than 40 KB are smaller than the minimum capacity charge per object in the S3 Glacier Deep Archive storage class\. These objects are stored in the S3 Standard storage class\. You must restore objects archived in this storage class before DataSync can read them\. For information, see [Working with archived objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/archived-objects.html) in the *Amazon S3 User Guide*\. When using S3 Glacier Deep Archive, choose **Verify only the data transferred** to compare data and metadata checksums at the end of the transfer\. **Verify all data in the destination** isn't an available option for this storage class, because it requires retrieving all existing objects from the destination\.   | 
|  S3 Outposts  |  The storage class for Amazon S3 on Outposts\.  | 

## Other considerations with Amazon S3 locations<a name="create-s3-location-considerations"></a>

When using Amazon S3 with DataSync, remember the following:
+ Changes to object data or metadata are equivalent to deleting and replacing an object\. These changes result in additional charges in the following scenarios:
  + **When using object versioning** – Changes to object data or metadata create a new version of the object\.
  + **When using storage classes that can incur additional charges for overwriting, deleting, or retrieving objects** – Changes to object data or metadata result in such charges\. For more information, see [Storage class considerations with Amazon S3 locations](#using-storage-classes)\. 
+ When using object versioning in Amazon S3, running a DataSync task once might create more than one version of an Amazon S3 object\.
+ We recommend creating a multipart upload bucket policy for your S3 buckets to help control your storage costs\. For more information, see the [https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html#lc-expire-mpu](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html#lc-expire-mpu)\.

## Creating the location<a name="create-s3-location-how-to"></a>

To create the location, you need an existing S3 bucket\. If you don't have one, see [Getting started with Amazon S3](https://docs.aws.amazon.com/https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html) in the *Amazon S3 User Guide*\.

**To create an Amazon S3 location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Go to the **Locations** page and choose **Create location**\.

1. For **Location type**, choose **Amazon S3**\.

1. For **S3 bucket**, choose the bucket that you want to use as a location\. \(When creating your DataSync task later, you specify whether this location is a source or destination location\.\)

   If your S3 bucket is located on an AWS Outposts resource, you must specify an Amazon S3 access point\. For more information, see [Managing data access with Amazon S3 access points](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points.html) in the *Amazon S3 User Guide*\.

1. For **S3 storage class**, choose a storage class that you want your objects to use\.

   For more information, see [Storage class considerations with Amazon S3 locations](#using-storage-classes)\. DataSync by default uses the S3 Outposts storage class for Amazon S3 on Outposts\.

1. \(Amazon S3 on Outposts only\) For **Agents**, specify the Amazon Resource Name \(ARN\) of the DataSync agent on your Outpost\.

   For more information, see [Deploy your agent on AWS Outposts](deploy-agents.md#outposts-agent)\.

1. For **Folder**, enter a prefix in the S3 bucket that DataSync reads from or writes to \(depending on whether the bucket is a source or destination location\)\.
**Note**  
The prefix can't begin with a slash \(for example, `/photos`\) or include consecutive slashes, such as `photos//2006/January`\.

1. For **IAM role**, do one of the following:
   + Choose **Autogenerate** for DataSync to automatically create an IAM role with the permissions required to access the S3 bucket\.

     If DataSync previously created an IAM role for this S3 bucket, that role is chosen by default\.
   + Choose a custom IAM role that you created\. For more information, see [Manually creating an IAM role to access your Amazon S3 bucket](#create-role-manually)\.

1. \(Optional\) Choose **Add tag** to tag your Amazon S3 location\.

   A *tag* is a key\-value pair that helps you manage, filter, and search for your locations\. 

1. Choose **Create location**\.

## Using IAM policies to access your S3 bucket<a name="create-s3-location-iam"></a>

Depending on your S3 bucket's security settings, you may need to create a custom IAM policy that allows DataSync to access the bucket\.

**Topics**
+ [Manually creating an IAM role to access your Amazon S3 bucket](#create-role-manually)
+ [Preventing the cross\-service confused deputy problem](#create-s3-location-confused-deputy)
+ [Accessing S3 buckets using server\-side encryption](#create-s3-location-encryption)

### Manually creating an IAM role to access your Amazon S3 bucket<a name="create-role-manually"></a>

While DataSync can create an IAM role for you with the required S3 bucket permissions, you also can configure a role yourself\.

**To manually create an IAM role to access your Amazon S3 bucket**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the left navigation pane, under **Access management**, choose **Roles**, and then choose **Create role**\.

1. On the **Select trusted entity** page, for **Trusted entity type**, choose **AWS service**\.

1. For **Use case**, choose **DataSync** in the dropdown list and select **DataSync \- S3 Location**\. Choose **Next**\.

1. On the **Add permissions** page, choose **AmazonS3FullAccess** for S3 buckets in AWS Regions\. Choose **Next**\.

   You can manually create a more restrictive policy than **AmazonS3FullAccess**\. Here's an example:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Action": [
                   "s3:GetBucketLocation",
                   "s3:ListBucket",
                   "s3:ListBucketMultipartUploads"
               ],
               "Effect": "Allow",
               "Resource": "YourS3BucketArn"
           },
           {
               "Action": [
                   "s3:AbortMultipartUpload",
                   "s3:DeleteObject",
                   "s3:GetObject",
                   "s3:ListMultipartUploadParts",
                   "s3:GetObjectTagging",
                   "s3:PutObjectTagging",
                   "s3:PutObject"
                 ],
               "Effect": "Allow",
               "Resource": "YourS3BucketArn/*"
           }
       ]
   }
   ```

   For Amazon S3 on Outposts, use the following policy:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Action": [
                   "s3-outposts:ListBucket",
                   "s3-outposts:ListBucketMultipartUploads"
               ],
               "Effect": "Allow",
               "Resource": [
                   "s3OutpostsBucketArn",
                   "s3OutpostsAccessPointArn"
               ],
               "Condition": {
                   "StringLike": {
                       "s3-outposts:DataAccessPointArn": "s3OutpostsAccessPointArn"
                   }
               }
           },
           {
               "Action": [
                   "s3-outposts:AbortMultipartUpload",
                   "s3-outposts:DeleteObject",
                   "s3-outposts:GetObject",
                   "s3-outposts:ListMultipartUploadParts",
                   "s3-outposts:GetObjectTagging",
                   "s3-outposts:PutObjectTagging"
               ],
               "Effect": "Allow",
               "Resource": [
                   "s3OutpostsBucketArn/*",
                   "s3OutpostsAccessPointArn"
               ],
               "Condition": {
                   "StringLike": {
                       "s3-outposts:DataAccessPointArn": "s3OutpostsAccessPointArn"
                   }
               }
           },
           {
               "Effect": "Allow",
               "Action": [
                   "s3-outposts:GetAccessPoint"
               ],
               "Resource": "s3OutpostsAccessPointArn"
           }
       ]
   }
   ```

1. Give your role a name and choose **Create role**\.

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. Select the refresh button next to the IAM role setting and then choose the role that you just created\.

### Preventing the cross\-service confused deputy problem<a name="create-s3-location-confused-deputy"></a>

To prevent the [cross\-service confused deputy problem](cross-service-confused-deputy-prevention.md), we recommend using the `aws:SourceArn` and `aws:SourceAccount` global condition context keys in your IAM role's trust policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "datasync.amazonaws.com"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "123456789012"
                },
                "StringLike": {
                    "aws:SourceArn": "arn:aws:datasync:us-east-2:123456789012:*"
                }
            }
        }
    ]
}
```

### Accessing S3 buckets using server\-side encryption<a name="create-s3-location-encryption"></a>

DataSync can copy data to or from [S3 buckets that use server\-side encryption](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html)\. The type of encryption key a bucket uses can determine if you need a custom policy allowing DataSync to access the bucket\.

When using DataSync with S3 buckets that use server\-side encryption, remember the following:
+ **If your S3 bucket is encrypted with an AWS managed key** – DataSync can access the bucket's objects by default if all your resources are in the same AWS account\.
+ **If your S3 bucket is encrypted with a customer\-managed AWS Key Management Service \(AWS KMS\) key \(SSE\-KMS\)** – The [key's policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html) must include the IAM role that DataSync uses to access the bucket\.
+ **If your S3 bucket is encrypted with a customer\-managed SSE\-KMS key and in a different AWS account** – DataSync needs permission to access the bucket in the other AWS account\. You can set up this up by doing the following:
  + In the IAM role used by DataSync, [specify the SSE\-KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/cmks-in-iam-policies.html) associated with the destination bucket\.
  + In the SSE\-KMS key's policy, [specify the IAM role used by DataSync](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html)\.
+ **If your S3 bucket is encrypted with a customer\-provided encryption key \(SSE\-C\)** – DataSync can't access this bucket\.

#### Example: SSE\-KMS key policy for DataSync<a name="create-s3-location-encryption-example"></a>

The following example is a [key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html) for a customer\-managed SSE\-KMS key\. The policy is associated with an S3 bucket that uses server\-side encryption\. The following values are specific to your setup:
+ *your\-account* – Your AWS account\.
+ *your\-admin\-role* – The IAM role that can administer the key\. \(This can also be an IAM user\.\)
+ *your\-datasync\-role* – The IAM role that allows DataSync to use the key when accessing the bucket\.

```
{
    "Id": "key-consolepolicy-3",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::your-account:root"
            },
            "Action": "kms:*",
            "Resource": "*"
        },
        {
            "Sid": "Allow access for Key Administrators",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::your-account:role/your-admin-role"
            },
            "Action": [
                "kms:Create*",
                "kms:Describe*",
                "kms:Enable*",
                "kms:List*",
                "kms:Put*",
                "kms:Update*",
                "kms:Revoke*",
                "kms:Disable*",
                "kms:Get*",
                "kms:Delete*",
                "kms:TagResource",
                "kms:UntagResource",
                "kms:ScheduleKeyDeletion",
                "kms:CancelKeyDeletion"
            ],
            "Resource": "*"
        },
        {
            "Sid": "Allow use of the key",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::your-account:role/your-datasync-role"
            },
            "Action": [
                "kms:Encrypt",
                "kms:Decrypt",
                "kms:ReEncrypt*",
                "kms:DescribeKey",
                "kms:GetPublicKey"
            ],
            "Resource": "*"
        },
        {
            "Sid": "Allow attachment of persistent resources",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::your-account:role/your-datasync-role"
            },
            "Action": [
                "kms:CreateGrant",
                "kms:ListGrants",
                "kms:RevokeGrant"
            ],
            "Resource": "*",
            "Condition": {
                "Bool": {
                    "kms:GrantIsForAWSResource": "true"
                }
            }
        }
    ]
}
```