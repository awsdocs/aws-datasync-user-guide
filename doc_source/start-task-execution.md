# Starting an AWS DataSync task with the AWS CLI<a name="start-task-execution"></a>

When a task execution starts, the task execution changes from **LAUNCHING** to **PREPARING** status within about 10 minutes\. The time that the task execution takes to move through its other phases is proportional to the size of your volume\. For information about task execution phases, see [Task execution](how-datasync-works.md#task-executions)\.

Use the following command to start a task execution\.

```
aws datasync start-task-execution \
    --task-arn 'arn:aws:datasync:region:account-id:task/task-id'
```

The command returns a task execution Amazon Resource Name \(ARN\) similar to the one shown following\.

```
{ 
    "TaskExecutionArn": "arn:aws:datasync:us-east-1:209870788375:task/task-08de6e6697796f026/execution/exec-04ce9d516d69bd52f"
}
```

You can override the task's options by specifying different options for the current execution, as shown in the example following\. For a description of these options, see [Options](API_Options.md)\.

```
aws datasync start-task-execution [...] \
    --override-options \
    --VerifyMode=NONE,OverwriteMode=NEVER,PosixPermissions=NONE
```

When you run a task, you can optionally configure the task to include specific files, folders, and objects to transfer\. For more information, see [Filtering data transferred by AWS DataSync](filtering.md)\.

**Note**  
Each agent can run a single task at a time\.