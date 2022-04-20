# Working with task executions in DataSync<a name="working-with-task-executions"></a>

In AWS DataSync, a *task execution* is an individual run of a task, which includes information such as start time, end time, bytes written, and status\. 

After a task execution starts, you can monitor its progress, add or adjust bandwidth throttling for it, or cancel it before it completes\.

**Topics**
+ [Adjusting bandwidth throttling for a task execution](#adjust-bandwidth-throttling)
+ [Task execution statuses](#understand-task-execution-statuses)
+ [Canceling a DataSync task execution](#cancel-running-task)

## Adjusting bandwidth throttling for a task execution<a name="adjust-bandwidth-throttling"></a>

You can modify bandwidth throttling for a task execution using the AWS Management Console or the DataSync API\. For information about using the API, see [UpdateTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_UpdateTaskExecution.html)\.

**To modify bandwidth throttling**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Tasks**\.

1. Select the **Task ID** for the running task that you want to monitor\. Using the console, you can modify any task execution that is currently running or that is queued\.

1. Choose **History** to view task execution instances\. 

1. Select the active task execution to be modified\.

1. For **Action**, choose **Edit**\.

1. In the **Edit Task Execution** dialog box that appears, choose **Use available** to remove bandwidth throttling and use all available bandwidth for the task execution\.

   Choose **Set bandwidth limit \(MIB/s\)** to change the bandwidth limit\.

   To save changes to your task execution's bandwidth limit, choose **Save changes**\. The new bandwidth limit setting goes into effect on the running or queued task execution within 60 seconds\.

## Task execution statuses<a name="understand-task-execution-statuses"></a>

Following, you can find information about the possible statuses \(phases\) a task execution might go through\.


| DataSync phase or status | Meaning | 
| --- | --- | 
|  **QUEUEING**  |  This is the first phase of a task execution if there is another task running and it's using the same agent\. For more information, see [Queueing task executions](run-task.md#queue-task-execution)\.  | 
|  **LAUNCHING**  |  This is the first phase of a task execution if there is no other task running and using the same agent or if queueing isn't enabled\. At this point, AWS DataSync is initializing the task execution\. This status usually goes quickly, but can take up to a few minutes\.  | 
|  **PREPARING**  |  This is the second phase of a task execution\. AWS DataSync is computing which files need to be transferred\. The time that this phase takes is proportional to the number of files in the source location\. It usually takes between a few minutes to a few hours, depending on both the source and destination file systems and the performance of these file systems\. For more information, see [Starting your DataSync task](run-task.md)\.  | 
|  **TRANSFERRING**  |  This is the third phase of a task execution\. DataSync is performing the actual transfer of your data to AWS\. While the DataSync is transferring files, the number of bytes and files that are transferred is updated in real time\.  | 
|  **VERIFYING**  |  This is the fourth and optional phase of a task execution\. If the `VerifyMode` sync option is set to **POINT\_IN\_TIME\_CONSISTENT**, DataSync performs a full data and metadata integrity verification\. This verification ensures that the data in your destination is an exact copy of the data in your source location\. This process requires reading back all files in the destination and can take a significant amount of time on very large volumes\. If you want to skip verification, specify `VerifyMode=NONE` when configuring the task execution\. Alternatively, in your task's options in the console, don't choose **Enable verification**\. For more information, see [How AWS DataSync verifies data integrity](how-datasync-works.md#how-verifying-works)\.  | 
|  **SUCCESS**  |  This value is returned if the data transfer is successful\. If the `VerifyMode` option isn't set, this status occurs after the **TRANSFERRING** phase\. Otherwise, it occurs after the **VERIFYING** phase\. For more information, see [Task execution](how-datasync-works.md#task-executions)\.  | 
|  **ERROR**  |  This value is returned if the data transfer fails\. If the `VerifyMode` option isn't set, this status occurs after the **TRANSFERRING** phase\. Otherwise, it occurs after the **VERIFYING** phase\.  | 

## Canceling a DataSync task execution<a name="cancel-running-task"></a>

 Using the console, you can cancel any task execution that is currently running or that is queued\. You can also cancel a task execution using the API\. For more information, see [CancelTaskExecution](https://docs.aws.amazon.com/datasync/latest/userguide/API_CancelTaskExecution.html)\. 

**To cancel a task execution**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Tasks**\.

1. Select the **Task ID** for the running task that you want to monitor\. The **Status** should be **Running**\.

1. Choose **History** to view task execution instances\.

1. Select the active task execution to be stopped\.

1. For **Action**, choose **Stop**\.

1. In the **Stop Task Execution** dialog box that appears, choose **Confirm** to stop the task execution\.