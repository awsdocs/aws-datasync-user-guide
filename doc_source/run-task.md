# Starting your DataSync task<a name="run-task"></a>

Starting a task creates a task execution\. A *task execution* is an individual run of a task\. Each task can have at most one task execution at a time\. You can run a task with the DataSync options already configured on the task level when creating it\. Alternatively, you can change the options for a specific task run and execution before you run the task\. For instructions on how to start a task, see [Start your task](run-your-task.md)\.

**Note**  
Each agent can execute a single task at a time\.

The time that AWS DataSync spends in the **PREPARING** status depends on the number of files in both the source and destination file systems\. It also depends on the performance of these file systems\. When a task starts, DataSync performs a recursive directory listing to discover all files and file metadata in the source and destination file system\. These listings are used to identify differences and determine what to copy, and usually takes between a few minutes to a few hours\.

## Queueing task executions<a name="queue-task-execution"></a>

When you use the same agent to run multiple tasks, you can queue one task execution for each task\. By using queueing, you can make tasks run in series \(first in, first out\) even if the agent is already running other tasks\. You can set queuing either by using the DataSync console or the API\.

You can queue multiple executions of the same task by using different filter settings for each task execution\. You can configure filter settings for a task execution using the **Start with overrides** option when you start a task\. For more information about filters, see [Filtering data transferred by AWS DataSync](filtering.md)\. 

To enable queueing on the DataSync console, choose **Enabled** for **Queueing** for the option when you configure task settings\. If you enable queueing and the agent is running an execution from another task or an execution using different filters, the current task's execution is automatically queued\. After a task execution finishes, DataSync runs the next queued execution\. If you want to remove a task execution from the queue yourself, cancel the execution\.

To enable queueing by using the DataSync API, set the `TaskQueueing` property to `ENABLED`\. 