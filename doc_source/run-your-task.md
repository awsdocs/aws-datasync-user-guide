# Start your task<a name="run-your-task"></a>

Next, you start your task\. You can further review your configuration settings before you start the task, 

**To start your task with the default configuration**

1. When the **Status** of the task changes from **Creating** to **Available**, choose **Start**, and then **Start with defaults**\.

1. The task starts and you are redirected to the **Task execution** page\.

**To start your task with a modified configuration**

1. When the **Status** of the task changes from **Creating** to **Available**, choose **Start**, and then **Start with overriding options**\.

1. The **Start task** page displays the default configuration\. You can choose to modify these settings before starting the task\. Any changes that you make are applied only to this task execution\.

1. After you review and make any changes to your task configuration, choose **Start**\. The task starts and you are redirected to the **Task execution** page\.

When you create a task, it first enters the **Creating** state\. While the task is in the **Creating** state, AWS DataSync performs validation checks on the source and destination locations\. After DataSync validates the locations, the task transitions to the **Available** state\. If an agent on the source location goes offline, the task transitions to the **Unavailable** state\.

For information about how DataSync transfers files, see [How DataSync transfers files](how-datasync-works.md#transfering-files)\.