# Start your task<a name="run-your-task"></a>

Next, you start your task\. You can further review your configuration settings before you start the task, 

**To start your task with the default configuration**

1. When the **Status** of the task changes from **Creating** to **Available**, choose **Start**\.

1. Choose **Start with defaults**\.

   The task starts and you're redirected to the **Task execution** page\.

**To start your task with a modified configuration**

1. When the **Status** of the task changes from **Creating** to **Available**, choose **Start**, and then **Start with overriding options**\.

1. Modify the settings that you want to change before starting the task\.

1. Review your changes and choose **Start**\.

   The task starts and you're redirected to the **Task execution** page\.

When you create a task, it first enters the **Creating** state\. While the task is in the **Creating** state, AWS DataSync performs validation checks on the source and destination locations\. After DataSync validates the locations, the task transitions to the **Available** state\. If an agent on the source location goes offline, the task transitions to the **Unavailable** state\.

For information about how DataSync transfers files, see [How DataSync transfers files and objects](how-datasync-works.md#transfering-files)\.