# Creating a task<a name="create-task-cli"></a>

After you have created an agent and configured your source and destination, you create a task, as described following\.

**To create a task by using the CLI**

1. Create an Amazon CloudWatch Logs log group by using the following command\.

   ```
   aws logs create-log-group \
       --log-group-name your-log-group
   ```

1. Attach an IAM resource policy to your log group\. For instructions on how to attach the policy, see [Allowing DataSync to upload logs to Amazon CloudWatch log groups](monitor-datasync.md#cloudwatchlogs)\. 

1. Create a task by using the following command\.

   ```
   aws datasync create-task \
       --source-location-arn 'arn:aws:datasync:region:account-id:location/location-id' \
       --destination-location-arn 'arn:aws:datasync:region:account-id:location/location-id' \
       --cloud-watch-log-group-arn 'arn:aws:logs:region:account-id:log-group:log-group' \
       --name task-name
   ```

   This command returns the Amazon Resource Name \(ARN\) for a task, similar to the one shown following\.

   ```
   { 
       "TaskArn": "arn:aws:datasync:us-east-1:111222333444:task/task-08de6e6697796f026" 
   }
   ```

   **When creating a task that transfers data between AWS services in different Regions**, and the other location needs to be specified in a different Region \(for example, to transfer data between `us-east-1` and `us-east-2`\), use DataSync in one of the Regions and create a task by using the following command\.

   You can transfer data between AWS Regions, except for the China Regions and the AWS GovCloud \(US\) Regions\. You can also transfer data between the AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\) Regions\. 

   ```
   aws datasync create-task \
       --source-location-arn 'arn:aws:datasync:us-east-1:account-id:location/location-id \
       --destination-location-arn 'arn:aws:datasync:us-east-2:account-id:location/location-id \
       --cloud-watch-log-group-arn 'arn:aws:logs:region:account-id' \
       --name task-name \
       --options VerifyMode=NONE,OverwriteMode=NEVER,Atime=BEST_EFFORT,Mtime=PRESERVE,Uid=INT_VALUE,Gid=INT_VALUE,PreserveDevices=PRESERVE,PosixPermissions=PRESERVE,PreserveDeletedFiles=PRESERVE,TaskQueueing=ENABLED,LogLevel=TRANSFER
   ```

   Your task is created with the default configuration options\. If you want to configure different options as part of your task creation, add the `--options` parameter to your `create-task` command\. The following example shows how to specify different options\. For a description of these options, see [Options](API_Options.md)\. 

   ```
   aws datasync create-task \
       --source-location-arn 'arn:aws:datasync:region:account-id:location/location-id' \
       --destination-location-arn 'arn:aws:datasync:region:account-id:location/location-id' \
       --cloud-watch-log-group-arn 'arn:aws:logs:region:account-id:log-group:log-group' \
       --name task-name \
       --options VerifyMode=NONE,OverwriteMode=NEVER,Atime=BEST_EFFORT,Mtime=PRESERVE,Uid=INT_VALUE,Gid=INT_VALUE,PreserveDevices=PRESERVE,PosixPermissions=PRESERVE,PreserveDeletedFiles=PRESERVE,TaskQueueing=ENABLED,LogLevel=TRANSFER
   ```

   When you create a task, you can configure the task to include or exclude specific files, folders, and objects\. For more information, see [Filtering the data transferred by DataSync](filtering.md)\. You can also schedule when you want your task to run\. For more information, see [Scheduling your DataSync task](task-scheduling.md)\.
**Note**  
If a task remains in the **CREATING** status for more than a few minutes, your agent might be having trouble reaching your self\-managed storage\. Check the task's `ErrorCode` and `ErrorDetail` values\. For example, NFS and SMB mount issues are often caused by a mistyped server hostname, or when the agent's access to your storage is blocked by firewall rules\.