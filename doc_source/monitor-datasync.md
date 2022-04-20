# Monitoring AWS DataSync<a name="monitor-datasync"></a>

**Topics**
+ [Accessing Amazon CloudWatch metrics for DataSync](#accessing-metrics)
+ [DataSync CloudWatch metrics](#metrics)
+ [CloudWatch events for DataSync](#events)
+ [DataSync dimensions](#cw-dimentions)
+ [Allowing DataSync to upload logs to Amazon CloudWatch log groups](#cloudwatchlogs)

You can monitor AWS DataSync using Amazon CloudWatch, which collects and processes raw data from DataSync into readable, near real\-time metrics\. These statistics are retained for a period of 15 months\. By default, DataSync metric data is automatically sent to CloudWatch at 5\-minute periods\. For more information about CloudWatch, see [What are Amazon CloudWatch, CloudWatch Events, and CloudWatch logs?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

## Accessing Amazon CloudWatch metrics for DataSync<a name="accessing-metrics"></a>

Amazon CloudWatch provides metrics that you can use to get information about DataSync performance\. You can see CloudWatch metrics for DataSync in many ways\. You can view them through the CloudWatch console, or you can access them using the CloudWatch CLI or the CloudWatch API\. You can also see these metrics on the task execution details page in the AWS DataSync console\. For information about how to use CloudWatch metrics, see [Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) in the *Amazon CloudWatch User Guide\.*

## DataSync CloudWatch metrics<a name="metrics"></a>

The `AWS/DataSync` namespace includes the following metrics\.

These statistics are retained for a period of 15 months\.


| Metric | Description | 
| --- | --- | 
| `BytesVerifiedSource` | The total number of bytes of data that are verified at the source location\. Units: Bytes  | 
| `BytesPreparedSource` | The total number of bytes of data that are prepared at the source location\. Unit: Bytes  | 
| `FilesVerifiedSource` | The total number of files that are verified at the source location\. Unit: Count  | 
| `FilesPreparedSource` | The total number of files that are prepared at the source location\. Unit: Count  | 
| `BytesVerifiedDestination` | The total number of bytes of data that are verified at the destination location\. Unit: Bytes  | 
| `BytesPreparedDestination` | The total number of bytes of data that are prepared at the destination location\. Unit: Bytes  | 
| `FilesVerifiedDestination` | The total number of files that are verified at the destination location\. Unit: Count  | 
| `FilesPreparedDestination` | The total number of files that are prepared at the destination location\. Unit: Count  | 
| `FilesTransferred` | The actual number of files or metadata that were transferred over the network\. This value is calculated and updated on an ongoing basis during the TRANSFERRING phase\. It's updated periodically when each file is read from the source location and sent over the network\. If failures occur during a transfer, this value can be less than `EstimatedFilesToTransfer`\. This value can also be greater than `EstimatedFilesTransferred` in some cases\. This element is implementation\-specific for some location types, so don't use it as an indicator for a correct file number or to monitor your task execution\.  Unit: Count  | 
| `BytesTransferred` | The total number of bytes that are transferred over the network when the agent reads from the source location to the destination location\. Unit: Bytes  | 
| `BytesWritten` | The total logical size of all files that have been transferred to the destination location\. Unit: Bytes  | 

## CloudWatch events for DataSync<a name="events"></a>

Amazon CloudWatch events describe changes in DataSync resources\. You can set up rules to match these events and route them to one or more target functions or streams\. Events are emitted on a best effort basis\. 

The following CloudWatch events are available for AWS DataSync\.


| Event | Description | 
| --- | --- | 
|  State Changes for an Agent  | For details, see [DataSync agent statuses](understand-agent-statuses.md)\. | 
| ONLINE | The agent is configured properly and is available to use\. The ONLINE status is the normal running status for an agent\.  | 
| OFFLINE | The agent's VM is turned off or the agent is in an unhealthy state and has been out of contact with the service for 5 minutes or longer\. When the issue that caused the unhealthy state is resolved, the agent returns to ONLINE status\. | 
| State Changes for a Location | 
| ADDING | DataSync is adding a location\. | 
| AVAILABLE | The location is created and is available to use\. | 
| State Changes for a Task  | For details, see [DataSync task creation statuses](understand-task-creation-statuses.md)\. | 
| CREATING | DataSync attempts to mount the Network File System \(NFS\) location and create the task\. | 
| RUNNING | DataSync has mounted the source and it is functioning properly\.  | 
| AVAILABLE | The task is configured properly and is available to be started\. | 
| UNAVAILABLE | The task is not configured properly and is not available for use\. If an agent that is associated with a source \(NFS\) location goes offline, the task transitions to the UNAVAILABLE status\.  | 
|  State Changes for a Task Execution  | 
| LAUNCHING | DataSync is initializing the task execution\. | 
| PREPARING | DataSync is computing which files need to be transferred\.  | 
| TRANSFERRING |  DataSync is performing the actual transfer of your data to AWS | 
| VERIFYING | DataSync performs a full data and metadata integrity verification to ensure that the data in your destination is an exact copy of your source\. | 
| SUCCESS | The transfer is successful\. | 
| ERROR | The sync has failed\. | 

## DataSync dimensions<a name="cw-dimentions"></a>

DataSync metrics use the `AWS/DataSync` namespace and provide metrics for the following dimensions:
+ AgentId—the unique ID of the agent\.
+ TaskId—the unique ID of the task\. It takes the form `task-01234567890abcdef`\.

## Allowing DataSync to upload logs to Amazon CloudWatch log groups<a name="cloudwatchlogs"></a>

You can use CloudWatch log groups to monitor and debug your tasks\. To upload logs to your log group, DataSync requires a resource policy that grants sufficient permissions\. When you create a task using the AWS Management Console, DataSync can automatically create the required resource policy\. For more information, see [Configure task settings](create-task.md)\. 

The following is an example resource policy that grants such permissions\.

```
{
    "Statement": [
        {
            "Sid": "DataSyncLogsToCloudWatchLogs",
            "Effect": "Allow",
            "Action": [
                "logs:PutLogEvents",
                "logs:CreateLogStream"
            ],
            "Principal": {
                "Service": "datasync.amazonaws.com"
            },
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": [
                        "arn:aws:datasync:region:account-id:task/*"
                    ]
                },
                "StringEquals": {
                    "aws:SourceAccount": "account-id"
                }
            },
            "Resource": "arn:aws:logs:region:account-id:log-group:*:*"
        }
    ],
    "Version": "2012-10-17"
}
```

The policy uses condition statements to ensure that only DataSync tasks from the specified account have access to the specified CloudWatch log group\. We recommend using the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys in these condition statements to protect against the confused deputy problem\. For more information, see [Cross\-service confused deputy prevention](cross-service-confused-deputy-prevention.md)\.

To specify the DataSync task or tasks, replace *`region`* with the Region code for the AWS Region where the tasks are located and replace *`account-id`* with the AWS account ID of the account that contains the tasks\. To specify the CloudWatch log group, replace the same values\. You can also modify the `Resource` statement to target specific log groups\. For more information about using `SourceArn` and `SourceAccount`, see [Global condition keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) in the *IAM User Guide*\.

To apply the policy, save this policy statement to a file on your local computer\. Then run the following AWS Command Line Interface \(AWS CLI\) command to apply the resource policy:

```
aws logs put-resource-policy --policy-name trustDataSync --policy-document file://full-path-to-policy-file
```

**Note**  
Run this command using the same AWS account and Region that your DataSync agent is activated in\.

For information about CloudWatch log groups, see [Working with log groups and log streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch Logs User Guide*\. 