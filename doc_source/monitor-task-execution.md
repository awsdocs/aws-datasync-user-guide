# Monitoring your task<a name="monitor-task-execution"></a>

To monitor the status of your task execution with the CLI, use the `describe-task-execution` command\.

```
aws datasync describe-task-execution \
    --task-execution-arn 'arn:aws:datasync:region:account-id:task/task-id/execution/task-execution-id'
```

This command returns information about a task execution similar to that shown following\.

```
{
    "TaskExecutionArn": "arn:aws:datasync:us-east-1:112233445566:task/task-08de6e6697796f026/execution/exec-04ce9d516d69bd52f",
    "Status": "VERIFYING",
    "Options": {
        "VerifyMode": "POINT_IN_TIME_CONSISTENT",
        "Atime": "BEST_EFFORT",
        "Mtime": "PRESERVE",
        "Uid": "INT_VALUE",
        "Gid": "INT_VALUE",
        "PreserveDevices": "NONE",
        "PosixPermissions": "PRESERVE",
        "PreserveDeletedFiles": "PRESERVE"
        "OverwriteMode": "NEVER",
        "TaskQueueing": "ENABLED"
    },
    "StartTime": 1532658526.949,
    "EstimatedFilesToTransfer": 0,
    "EstimatedBytesToTransfer": 0,
    "FilesTransferred": 0,
    "BytesWritten": 0,
    "BytesTransferred": 0,
    "Result": {
        "PrepareDuration": 4355,
        "PrepareStatus": "Ok",
        "TransferDuration": 5889,
        "TransferStatus": "Ok",
        "VerifyDuration": 4538,
        "VerifyStatus": "Pending"
    }
}
```

If the task execution succeeds, the value of **Status** changes to **SUCCESS**\. If the `describe-task-execution` command fails, the result sends error codes that can help you troubleshoot issues\. For information about the error codes, see [TaskExecutionResultDetail](API_TaskExecutionResultDetail.md) in the *DataSync API Reference\.*

## Monitoring your task in real time<a name="monitor-realtime"></a>

To monitor the progress of your task execution in real time from the command line, use the standard Unix `watch` utility\. Task execution duration values are measured in milliseconds\.

The `watch` utility doesn't recognize the DataSync alias, so invoke the CLI directly as shown in the following example\.

```
# pass '-n 1' to update every second and '-d' to highlight differences 
$ watch -n 1 -d \ "aws datasync describe-task-execution --task-execution-arn 'arn:aws:datasync:region:account-id:task/task-id/execution/task execution-id'"
```