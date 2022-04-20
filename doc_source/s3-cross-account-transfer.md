# Tutorial: Transferring data from on\-premises storage to Amazon S3 in a different AWS account<a name="s3-cross-account-transfer"></a>

When using AWS DataSync with on\-premises storage, you typically copy data to an AWS storage service that belongs to the same AWS account as your DataSync agent\. There are situations, however, where you might need to transfer data to an Amazon S3 bucket that's associated with a different account\.

## Overview<a name="s3-cross-account-overview"></a>

In this tutorial, you’ll learn how AWS Identity and Access Management \(IAM\) and the AWS Command Line Interface \(AWS CLI\) can help you create DataSync tasks that transfer data from on\-premises storage to an S3 bucket in a different AWS account\.

Here's what this kind of scenario can look like:
+ **Account A**: The AWS account that you use for managing network resources\. The endpoint that you activate the DataSync agent with also belongs to this account\. 
**Note**  
The steps in this tutorial apply to [any type of endpoint](choose-service-endpoint.md) that you activate your agent with\.
+ **Account B**: The account for the S3 bucket that you want to copy data to\.

The following diagram illustrates this scenario\. 

![\[An example DataSync scenario of data moving from an on-premises storage system across the internet into AWS. The data is first transferred into one AWS account (Account A), before finally making it into an Amazon S3 bucket in a different AWS account (Account B).\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/s3-cross-account-diagram.png)

**Important**  
Copying data across AWS accounts by using the methods in this tutorial works only when Amazon S3 is one of the DataSync locations\.

## Prerequisites<a name="s3-cross-account-prerequisites"></a>

Before you begin the IAM work to facilitate the cross\-account transfer, do the following if you already haven't:

1. [Configure your network](datasync-network.md) so that your on\-premises storage system can connect with AWS\.

1. [Deploy and activate your DataSync agent](activating-agent.md) by using Account A\.

1. [Create a DataSync source location](working-with-locations.md) by using Account A for the on\-premises storage system that you're copying data from\.

1. [Set up the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) by using Account A\. You'll need the AWS CLI to create the DataSync destination location for the S3 bucket in Account B\.

## Step 1: Create an IAM role for DataSync in Account A<a name="s3-cross-account-create-iam-role-account-a"></a>

You need an IAM role that gives DataSync permission to write to the S3 bucket in Account B\. DataSync assumes this role when copying the data across accounts\. For more information, see [Creating a role for an AWS service \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html#roles-creatingrole-service-console) in the *IAM User Guide*\.

### Create the IAM role<a name="s3-cross-account-create-iam-role"></a>

Create a role with DataSync as the trusted entity\.

**To create the IAM role**

1. Log in to the AWS Management Console with Account A\.

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the left navigation pane, under **Access management**, choose **Roles**, and then choose **Create role**\.

1. On the **Select trusted entity** page, for **Trusted entity type**, choose **AWS service**\.

1. For **Use case**, choose **DataSync** in the dropdown list, and then choose **DataSync**\. Choose **Next**\.

1. On the **Add permissions** page, choose **Next**\.

1. Give your role a name and choose **Create role**\.

### Attach a custom policy to the IAM role<a name="s3-cross-account-attach-custom-policy"></a>

The IAM role needs a policy that allows DataSync to write to your S3 bucket in Account B\.

**To attach a custom policy to the IAM role**

1. On the **Roles** page of the IAM console, search for the role that you just created and choose its name\.

1. On the role's details page, choose the **Permissions** tab\. Choose **Add permissions**, and then choose **Create inline policy**\.

1. Choose the **JSON** tab and then do the following:

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

1. Give your policy a name, and choose **Create policy**\.

## Step 2: Disable ACLs for your S3 bucket in Account B<a name="s3-cross-account-disable-acls-account-b"></a>

It's important that all the data that you copy to the S3 bucket belongs to Account B\. To ensure that Account B is the owner of the data, make sure to disable the bucket's access control lists \(ACLs\)\. For more information, see [Controlling ownership of objects and disabling ACLs for your bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/about-object-ownership.html) in the *Amazon S3 User Guide*\.

**To disable ACLs for an S3 bucket**

1. In the AWS Management Console, switch over to Account B\.

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\. 

1. In the **Buckets** list, choose the S3 bucket that you're transferring data to\.

1. On the bucket's detail page, choose the **Permissions** tab\.

1. Under **Object Ownership**, choose **Edit**\.

1. If it isn't already selected, choose the **ACLs disabled \(recommended\)** option\.

1. Choose **Save changes**\.

## Step 3: Update the S3 bucket policy in Account B<a name="s3-cross-account-update-s3-policy-account-b"></a>

In Account B, modify the S3 bucket policy to allow access to the IAM role that you created for DataSync in Account A\.

The updated policy \(provided to you in the following instructions\) includes two service principals:
+ The first principal specifies the IAM role that you created in Account A that allows DataSync to write to the S3 bucket\.
+ The second principal specifies the IAM user name for Account A, which allows you to create the DataSync destination for the S3 bucket by using the AWS CLI \(you'll do this in Step 4\)\.

**To update the S3 bucket policy**

1. While still in the S3 console and using Account B, choose the S3 bucket that you're copying data to\.

1. On the bucket's detail page, choose the **Permissions** tab\.

1. Under **Bucket policy**, choose **Edit**, and do the following to modify your S3 bucket policy:

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

   1. Replace `name-of-user` with the IAM user name for Account A\.

   1. Replace `account-b-bucket` with the name of the S3 bucket in Account B\.

1. Choose **Save changes**\.

## Step 4: Create a DataSync destination location for the S3 bucket<a name="s3-cross-account-create-datasync-destincation"></a>

After you create a location for the S3 bucket, you can run your DataSync task\. The DataSync console, however, doesn’t support creating locations in different accounts\. You must create the location with the AWS CLI instead\.

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

## Step 5: Create and start your DataSync task<a name="s3-cross-account-create-start-datasync-task"></a>

Before you move your data, let's recap what you've done so far:
+ Deployed and activated your DataSync agent in Account A so that the agent can read from your self\-managed storage system and communicate with AWS\.
+ Created an IAM role in Account A so that DataSync can write data to the S3 bucket in Account B\.
+ Configured your S3 bucket in Account B to ensure that your DataSync task works\.
+ Created your DataSync source and destination locations in Account A\.

**To create and start your DataSync task**

1. While still using the DataSync console in Account A, choose **Tasks** in the left navigation pane, and then choose **Create task**\.

1. On the **Configure source location** page, choose **Choose an existing location**, and then choose the source location that you're copying data from \(your on\-premises storage\), and then choose **Next**\.

1. On the **Configure destination location** page, choose **Choose an existing location**, and then choose the destination location that you;re copying data to \(the S3 bucket in Account B\), and choose **Next**\.

1. On the **Configure settings** page, give the task a name\. As needed, configure additional settings, such as specifying an Amazon CloudWatch log group\. Choose **Next**\.

1. On the **Review** page, review your settings, choose **Create task**\.

1. On the task's details page, choose **Start**, and then choose either **Start with defaults** or **Start with overriding options**\. 

When your task is finished, you'll see the data from your on\-premises storage in the S3 bucket\. You can now access the bucket data from Account B\.

## Related resources<a name="s3-cross-account-create-start-datasync-task"></a>

For more information about what you did in this tutorial, see the following topics:
+ [Creating a role for an AWS service \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html#roles-creatingrole-service-console)
+ [Modifying a role trust policy \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-editing-console.html#roles-managingrole_edit-trust-policy)
+ [Adding a bucket policy by using the Amazon S3console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html)
+ [Create an S3 location with the AWS CLI](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/datasync/create-location-s3.html)