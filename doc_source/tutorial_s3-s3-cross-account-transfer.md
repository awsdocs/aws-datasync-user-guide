# Tutorial: Transferring data from Amazon S3 to Amazon S3 in a different AWS account<a name="tutorial_s3-s3-cross-account-transfer"></a>

With AWS DataSync, you can move data between Amazon S3 buckets that belong to different AWS accounts\.

**Important**  
Copying data across AWS accounts using the methods in this tutorial works only with Amazon S3\.

## Overview<a name="s3-s3-cross-account-overview"></a>

In this tutorial, you’ll learn how AWS Identity and Access Management \(IAM\) and the AWS Command Line Interface \(AWS CLI\) can help you create DataSync tasks that transfer data from Amazon S3 to another S3 bucket in a different AWS account\.

**Tip**  
Follow this tutorial if your S3 buckets are also in different AWS Regions\. The process is mostly the same except for some extra steps\. Keep in mind, however, that DataSync doesn't support these kinds of transfers for [Regions disabled by default](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html)\.

Here's what this kind of scenario can look like:
+ **Account A**: The AWS account that you use for managing the S3 bucket that you want to copy data from\.
+ **Account B**: The AWS account that you use for managing the S3 bucket that you want to copy data to\.

------
#### [ Transfers across accounts ]

The following diagram illustrates a scenario where you copy data from an S3 bucket to another S3 bucket that's in a different AWS account\.

![\[An example DataSync scenario of data moving from an S3 bucket in one AWS account (Account A) before making it into an S3 bucket in a different AWS account (Account B).\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/s3-s3-cross-account-same-region-diagram.png)

------
#### [ Transfers across accounts and Regions ]

The following diagram illustrates a scenario where you copy data from an S3 bucket to another S3 bucket that's in a different AWS account and Region\.

![\[An example DataSync scenario of data moving from an S3 bucket in one AWS account (Account A) and Region before making it into an S3 bucket in a different AWS account (Account B) and Region.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/s3-s3-cross-account-diff-region-diagram.png)

------

## Prerequisites<a name="s3-s3-cross-account-prerequisites"></a>

Before you begin the IAM work to facilitate the cross\-account transfer, do the following if you already haven't:

1. Determine how many objects you're copying\. Use [Amazon S3 Storage Lens](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage_lens.html) to figure out how many objects are in your bucket\.
**Tip**  
When transferring between S3 buckets, DataSync can't copy more than 25 million objects per task\. If your bucket has more than 25 million objects, we recommend a couple options:   
[Organizing your objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-prefixes.html) using prefixes that you don't include more than 25 million objects\. You can then create separate DataSync tasks for each prefix\.
[Filtering the data](filtering.md) transferred by DataSync\.

1. [Create a DataSync source location](create-s3-location.md) with Account A for the S3 bucket that you're copying data from\.

1. [Set up the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) with Account A\. You'll need the AWS CLI to create the DataSync destination location for the S3 bucket in Account B\.

## Step 1: Create an IAM role for DataSync in Account A<a name="s3-s3-cross-account-create-iam-role-account-a"></a>

You need an IAM role that gives DataSync permission to write to the S3 bucket in Account B\. 

When you create a location for a bucket, DataSync can automatically create and assume a role with the right permissions to access that bucket\. Since you're transferring across accounts, you must create the role manually\.

 For more information, see [Creating a role for an AWS service \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html#roles-creatingrole-service-console) in the *IAM User Guide*\.

### Create the IAM role<a name="s3-s3-cross-account-create-iam-role"></a>

Create a role with DataSync as the trusted entity\.

**To create the IAM role**

1. Log in to the AWS Management Console with Account A\.

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the left navigation pane, under **Access management**, choose **Roles**, and then choose **Create role**\.

1. On the **Select trusted entity** page, for **Trusted entity type**, choose **AWS service**\.

1. For **Use case**, choose **DataSync** in the dropdown list and select **DataSync**\. Choose **Next**\.

1. On the **Add permissions** page, choose **Next**\.

1. Give your role a name and choose **Create role**\.

### Attach a custom policy to the IAM role<a name="s3-s3-cross-account-attach-custom-policy"></a>

The IAM role needs a policy that allows DataSync to write to your S3 bucket in Account B\.

**To attach a custom policy to the IAM role**

1. On the **Roles** page of the IAM console, search for the role that you just created and choose its name\.

1. On the role's details page, choose the **Permissions** tab\. Choose **Add permissions** then **Create inline policy**\.

1. Choose the **JSON** tab and do the following:

   1. Paste the following JSON into the policy editor:

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
            "Resource": "arn:aws:s3:::account-b-bucket"
          },
          {
            "Action": [
              "s3:AbortMultipartUpload",
              "s3:DeleteObject",
              "s3:GetObject",
              "s3:ListMultipartUploadParts",
              "s3:PutObject",
              "s3:GetObjectTagging",
              "s3:PutObjectTagging"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::account-b-bucket/*"
          }
        ]
      }
      ```

   1. Replace `account-b-bucket` with the name of the S3 bucket in Account B\.

1. Choose **Review policy**\.

1. Give your policy a name and choose **Create policy**\.

## Step 2: Disable ACLs for your S3 bucket in Account B<a name="s3-s3-cross-account-disable-acls-account-b"></a>

It's important that all the data that you copy to the S3 bucket belongs to Account B\. To ensure that Account B is the owner of the data, disable the bucket's access control lists \(ACLs\)\. For more information, see [Controlling ownership of objects and disabling ACLs for your bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/about-object-ownership.html) in the *Amazon S3 User Guide*\.

**To disable ACLs for an S3 bucket**

1. In the AWS Management Console, switch over to Account B\.

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\. 

1. In the **Buckets** list, choose the S3 bucket that you're transferring data to\.

1. On the bucket's detail page, choose the **Permissions** tab\.

1. Under **Object Ownership**, choose **Edit**\.

1. If it isn't already selected, choose the **ACLs disabled \(recommended\)** option\.

1. Choose **Save changes**\.

## Step 3: Update the S3 bucket policy in Account B<a name="s3-s3-cross-account-update-s3-policy-account-b"></a>

In Account B, modify the S3 bucket policy to allow access to the IAM role that you created for DataSync in Account A\.

The updated policy \(provided to you in the following instructions\) includes two principals:
+ The first principal specifies the IAM role that you created in Account A that allows DataSync to write to the S3 bucket\.
+ The second principal specifies the IAM user name for Account A, which allows you to create the DataSync destination for the S3 bucket by using the AWS CLI \(you'll do this in Step 4\)\.
**Note**  
If you log in to the console and access the AWS CLI using an IAM role, specify that role instead of a user name for the second principal\.

**To update the S3 bucket policy**

1. While still in the S3 console and using Account B, choose the S3 bucket that you're copying data to\.

1. On the bucket's detail page, choose the **Permissions** tab\.

1. Under **Bucket policy**, choose **Edit** and do the following to modify your S3 bucket policy:

   1. Update what's in the editor to include the following policy statements:

      ```
      {
        "Version": "2008-10-17",
        "Statement": [
          {
            "Sid": "DataSyncCreateS3LocationAndTaskAccess",
            "Effect": "Allow",
            "Principal": {
              "AWS": "arn:aws:iam::account-a-id:role/name-of-role"
            },
            "Action": [
              "s3:GetBucketLocation",
              "s3:ListBucket",
              "s3:ListBucketMultipartUploads",
              "s3:AbortMultipartUpload",
              "s3:DeleteObject",
              "s3:GetObject",
              "s3:ListMultipartUploadParts",
              "s3:PutObject",
              "s3:GetObjectTagging",
              "s3:PutObjectTagging"
            ],
            "Resource": [
              "arn:aws:s3:::account-b-bucket",
              "arn:aws:s3:::account-b-bucket/*"
            ]
          },
          {
            "Sid": "DataSyncCreateS3Location",
            "Effect": "Allow",
            "Principal": {
              "AWS": "arn:aws:iam::account-a-id:user/name-of-user"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::account-b-bucket"
          }
        ]
      }
      ```

   1. Replace `account-a-id` with the AWS account number of Account A\.

   1. Replace `name-of-role` with the IAM role that you created for DataSync in Account A \(back in Step 1\)\.

   1. Replace `account-b-bucket` with the name of the S3 bucket in Account B\.

   1. Replace `name-of-user` with the IAM user name that you use to log in to the console with Account A\.

      If you're specifying an IAM role instead, update the format of the Amazon Resource Name \(ARN\):

      `"arn:aws:iam::account-a-id:role/name-of-role"`

1. Choose **Save changes**\.

## Step 4: Create a DataSync destination location for the S3 bucket<a name="s3-s3-cross-account-create-datasync-destincation"></a>

After you create a location for the S3 bucket, you can run your DataSync task\. The DataSync console, however, doesn’t support creating locations in different accounts\. You must create the location with the AWS CLI before you can run the task\.

**To create a DataSync location with the CLI**

1. Open a terminal\.

1. Make sure that your CLI profile is configured to use Account A\.

1. Copy the following command:

   ```
   aws datasync create-location-s3 --s3-bucket-arn arn:aws:s3:::account-b-bucket --s3-config '{"BucketAccessRoleArn":"arn:aws:iam::account-a-id:role/name-of-role"}'
   ```

1. Replace `account-b-bucket` with the name of the S3 bucket in Account B\.

1. Replace `account-a-id` with the AWS account number of Account A\.

1. Replace `name-of-role` with the IAM role that you created for DataSync in Account A \(back in Step 1\)\.

1. If the bucket in Account B is in a different Region than the bucket in Account A, add the `--region` option at the end of the command to specify the Region where there Account B bucket resides\. For example, `--region us-west-1`\.

1. Run the command\.

   If the command returns a DataSync location ARN similar to this, you successfully created the location:

   ```
   {
     "LocationArn": "arn:aws:datasync:us-east-2:123456789012:location/loc-abcdef01234567890"
   }
   ```

1. Switch back to Account A in the AWS Management Console\.

1. Open the DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**\.

   You can see the location of the S3 bucket in Account B that you just created with the CLI\.

## Step 5: Create and start a DataSync task<a name="s3-s3-cross-account-create-start-datasync-task"></a>

Before you move your data, let's recap what you've done so far:
+ Created an IAM role in Account A so that DataSync can write data to the S3 bucket in Account B\.
+ Configured your S3 bucket in Account B to ensure that your DataSync task works\.
+ Created your DataSync source and destination locations in Account A\.

**To create and start the DataSync task**

1. While still using the DataSync console in Account A, choose **Tasks** in the left navigation pane then **Create task**\.
**Note**  
You must be logged in to the console with the same IAM user name \(or role\) for Account A that you specified in the S3 bucket policy in Step 3\.

1. If the bucket in Account B is in a different Region than the bucket in Account A, choose the Account B bucket's Region in the navigation pane\.

   You must start the DataSync task from the Region of the destination location \(in this case, the Account B bucket\) to avoid a connection error\.

1. On the **Configure source location** page, choose **Choose an existing location**\.

1. For transfers across Regions, choose the Region where the Account A bucket resides\.

1. Choose the source location that you're copying data from \(the S3 bucket in Account A\) then **Next**\.

1. On the **Configure destination location** page, choose **Choose an existing location**\. Choose the destination location that you're copying data to \(the S3 bucket in Account B\) then **Next**\.

1. On the **Configure settings** page, give the task a name\. As needed, configure additional settings, such as specifying an Amazon CloudWatch log group\. Choose **Next**\.

1. On the **Review** page, review your settings and choose **Create task**\.

1. On the task's details page, choose **Start**, and then choose one of the following:
   + To run the task without modification, choose **Start with defaults**\.
   + To modify the task before running it, choose **Start with overriding options**\.

When your task finishes, check the S3 bucket in Account B\. You should see the data from your Account A bucket\.

## Related resources<a name="s3-s3-cross-account-create-start-datasync-task"></a>

For more information about what you did in this tutorial, see the following topics:
+ [Creating a role for an AWS service \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html#roles-creatingrole-service-console)
+ [Modifying a role trust policy \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-editing-console.html#roles-managingrole_edit-trust-policy)
+ [Adding a bucket policy by using the Amazon S3 console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html)
+ [Create an S3 location with the AWS CLI](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/datasync/create-location-s3.html)