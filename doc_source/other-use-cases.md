# Additional AWS DataSync use cases<a name="other-use-cases"></a>

In this section, you can find information about use cases in AWS DataSync that are not common to most users\.

**Topics**
+ [Transferring files in opposite directions](#opposite-direction-tasks)
+ [Using multiple tasks to write to the same Amazon S3 bucket](#multiple-tasks)
+ [Allowing DataSync to access a restricted Amazon S3 bucket](#denying-s3-access)

## Transferring files in opposite directions<a name="opposite-direction-tasks"></a>

Transferring data in opposite directions allows for workflows where the active application moves between locations\. AWS DataSync doesn't support workflows where multiple active applications write to both locations at the same time\. Use the steps in the following procedure to configure DataSync to transfer data in opposite directions\.

**To configure DataSync to data transfers in opposite directions**

1. Create a location and name it **Location A**\.

1. Create a second location and name it **Location B**\.

1. Create a task, name it **Task A\-B**, and then configure **Location A** as the source location and **Location B** as the destination location\.

1. Create a second task, name it **Task B\-A**, and then configure **Location B** as the source location and **Location A** as the destination location\.

1. To update **Location B** with data from **Location A**, run **Task A\-B**\.

   To update **Location A** with data from **Location B**, run **Task B\-A**\.

   Don't run these two tasks concurrently\. DataSync can transfer files in opposite directions periodically\. However, it doesn't support workflows where multiple active applications write to both **Location A** and **Location B** simultaneously\.

## Using multiple tasks to write to the same Amazon S3 bucket<a name="multiple-tasks"></a>

In certain use cases, you might want different tasks to write to the same Amazon S3 bucket\. In this case, you create different folders in the S3 bucket for each of the task\. This approach prevents file name conflicts between the tasks, and also means that you can set different permissions for each of folders\. 

For example, you might have three tasks: `task1`, `task2`, and `task3` write to an S3 bucket named `MyBucket`\.

You create three folders in the bucket:

`s3://MyBucket/task1`

`s3://MyBucket/task2`

`s3://MyBucket/task3`

For each task, you choose the folder in `MyBucket` that corresponds to the task as the destination, and set different permissions for each of the three folders\.

## Allowing DataSync to access a restricted Amazon S3 bucket<a name="denying-s3-access"></a>

In some cases, you might want to limit access to your Amazon S3 bucket\. You can edit the S3 bucket policy so that DataSync can still access the bucket when you run a task\.

**To allow DataSync to access a restricted S3 bucket**

1. Copy the following sample policy\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Deny",
         "Principal": "*",
         "Action": "s3:*",
         "Resource": [
           "arn:aws:s3:::bucket-name",
           "arn:aws:s3:::bucket-name/*"
         ],
         "Condition": {
           "StringNotLike": {
             "aws:userid": [
               "datasync-role-id:*",
               "datasync-user-id"
             ]
           }
         }
       }
     ]
   }
   ```

1. In the sample policy, replace these values:
   + *bucket\-name*: The name of the S3 bucket that you're restricting access to\.
   + *datasync\-role\-id*: The ID of the DataSync IAM role that needs access to the S3 bucket\. Get the IAM role ID by running the following AWS CLI command:

     `aws iam get-role --role-name datasync-iam-role-name`

     In the output, look for the `RoleId` value:

     `"RoleId": "ANPAJ2UCCR6DPCEXAMPLE"`
   + *datasync\-user\-id*: The ID of the IAM user creating the DataSync location for the S3 bucket\. \(If you're using a role to create the location, specify that role ID instead\.\) Get the IAM user ID by running the following AWS CLI command:

     `aws iam get-user`

     In the output, look for the `UserId` value:

     `"UserId": "AIDACKCEVSQ6C2EXAMPLE"`

1. Add this policy to your S3 bucket policy\. For more information, see how to [edit a bucket policy](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html) in the *Amazon S3 User Guide*\.

Once you've updated the S3 bucket policy, you must add additional IAM roles or users to the policy for those who need to access the S3 bucket\.