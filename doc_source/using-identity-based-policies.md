# Using identity\-based policies \(IAM policies\) for DataSync<a name="using-identity-based-policies"></a>

An account administrator can attach identity\-based policies to IAM identities \(that is, users, groups, and roles\)\. You can also attach identity\-based policies to service roles\.

This topic provides examples of identity\-based policies that you can use to grant permissions to IAM identities\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your DataSync resources\. For more information, see [Overview of managing access permissions for DataSync](managing-access-overview.md)\. 

The sections in this topic cover the following:
+ [AWS managed policies for DataSync](#access-policy-examples-aws-managed)
+ [Permissions required to use the DataSync console](#additional-console-required-permissions)
+ [Customer managed policy examples](#customer-managed-policies)

The following shows an example of a policy that grants permissions to use certain DataSync actions\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowsSpecifiedActionsOnAllTasks",
            "Effect": "Allow",
            "Action": [
                "datasync:DescribeTask",
                "datasync:ListTasks"
            ],
            "Resource": "arn:aws:datasync:us-east-2:111222333444:task/*"
        },    
}
```

The policy has one statement \(note the `Action` and `Resource` elements in the statement\) that does the following:
+ The statement grants permissions to perform two DataSync actions \(`datasync:DescribeTask` and `datasync:ListTasks`\) on certain task resources by using an *Amazon Resource Name \(ARN\)*\. 
+ In this statement, the task ARN specifies a wildcard character \(`*`\) because the IAM user, group, or role is allowed to perform the two actions on all tasks\. To limit permissions for the actions to a specific task, specify the task ID in the ARN instead of the wildcard character\. 

## AWS managed policies for DataSync<a name="access-policy-examples-aws-managed"></a>

AWS creates and administers standalone IAM policies\. These managed policies grant permissions for common use cases so that you can avoid investigating what permissions you need\. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The managed policies that are created by AWS grant the required permissions for common use cases\. You can attach these policies to your IAM users, groups, and roles, based on the access that they need to DataSync:

The following AWS managed policies, which you can attach to users in your account, are specific to DataSync:
+ **[AWSDataSyncReadOnlyAccess](https://console.aws.amazon.com/iam/home?#/policies/arn:aws:iam::aws:policy/AWSDataSyncReadOnlyAccess$jsonEditor)** – Provides read\-only access to AWS DataSync\. 
+ ** [AWSDataSyncFullAccess](https://console.aws.amazon.com/iam/home?#/policies/arn:aws:iam::aws:policy/AWSDataSyncFullAccess$jsonEditor)** – Provides full access to AWS DataSync and minimal access to its dependencies\.

 

**Note**  
You can review these managed policies by signing in to the IAM console and searching for specific policies there\.

You can also create your own custom IAM policies to allow permissions for AWS DataSync API actions\. You can attach these custom policies to the IAM users, groups, or roles that require those permissions\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

## Permissions required to use the DataSync console<a name="additional-console-required-permissions"></a>

To use the DataSync console, you must have [AWSDataSyncFullAccess](https://console.aws.amazon.com/iam/home?#/policies/arn:aws:iam::aws:policy/AWSDataSyncFullAccess$jsonEditor) permissions\.

## Customer managed policy examples<a name="customer-managed-policies"></a>

In this section, you can find example user policies that grant permissions for various DataSync actions\. These policies work when you are using the AWS SDKs and the AWS Command Line Interface \(AWS CLI\)\. When you are using the console, you must grant additional permissions specific to the console, which is discussed in [Permissions required to use the DataSync console](#additional-console-required-permissions)\.

**Note**  
All of these examples use fictitious account IDs and resource IDs\.

**Topics**
+ [Example 1: Create a trust relationship that allows DataSync to access your Amazon S3 bucket](#datasync-example1)
+ [Example 2: Allow DataSync to read and write to your Amazon S3 bucket](#datasync-example2)
+ [Example 3: Allow DataSync to upload logs to CloudWatch log groups](#datasync-example4)

### Example 1: Create a trust relationship that allows DataSync to access your Amazon S3 bucket<a name="datasync-example1"></a>

The following is an example of a trust policy that allows DataSync to assume an IAM role\. This role allows DataSync to access an Amazon S3 bucket\. To prevent the [cross\-service confused deputy problem](cross-service-confused-deputy-prevention.md), we recommend using the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys in the policy\.

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

### Example 2: Allow DataSync to read and write to your Amazon S3 bucket<a name="datasync-example2"></a>

The following example policy grants DataSync the minimum permissions to read and write data to your S3 bucket\.

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

### Example 3: Allow DataSync to upload logs to CloudWatch log groups<a name="datasync-example4"></a>

DataSync requires permissions to be able to upload logs to your Amazon CloudWatch log groups\. You can use CloudWatch log groups to monitor and debug your tasks\.

For an example of an IAM policy that grants such permissions, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\.

 