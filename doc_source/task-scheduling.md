# Scheduling your DataSync task<a name="task-scheduling"></a>

Using task scheduling in AWS DataSync, you can periodically execute a transfer task from your source storage system to the destination\. 

A scheduled task automatically runs at a frequency that you configure with a minimum interval of 1 hour\. For example, the following screenshot shows a configuration that runs a task every Sunday and Wednesday at 12:00 PM UTC\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/days-of-week-schedule.png)

You can also execute a task schedule using a cron expression specified in UTC time\. For example, configure a task to run on every Sunday and Wednesday at 12:00 PM by using the following cron expression\.

```
0 12 ? * SUN,WED *
```

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/cron-expression.png)

**Important**  
Even with a cron expression, you can't schedule a task to run at an interval faster than 1 hour\.

For detailed information about schedule expressions syntax, see [Schedule expressions for rules](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html#CronExpressions) in the *Amazon CloudWatch User Guide*\.

## Configuring a task schedule<a name="configure-task-schedule"></a>

You can configure the frequency of the task execution by using the DataSync console or API\. When you create or edit a task, the following options are available for **Frequency** in the console: 
+ Choose **Not Scheduled** if you don't want to schedule your task to run periodically\.
+ Choose **Hourly** and choose the minute in the hour that the task should run\. The task runs every hour on the specified minute\.
+ Choose **Daily** and enter the UTC time that you want the task to run, in the format HH:MM\. This task runs every day at the specified time\.
+ Choose **Weekly** and the day of the week and enter the UTC time the task should run, in the format HH:MM\. This task runs every week on the specified day at the specified time\.
+ Choose **Days of the week**, choose the specific day or days, and enter the UTC time that the task should run in the format HH:MM\. This task runs on the days and the time that you specified\.
+ Choose **Custom** if you want to use a custom cron expression to run your task, with a minimum interval of 1 hour\. Then enter your expression in the **Cron expression** box\. 

For detailed information about schedule expressions, see [Schedule expressions for rules](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html#CronExpressions) in the *Amazon CloudWatch User Guide*\.

## Editing a task schedule<a name="edit-task-schedule"></a>

You can configure scheduling when you [initially create a task](create-task.md), or you can edit a task schedule after a task is created\. Use the following procedure to configure a schedule after you have created a task\.

**To edit a task schedule**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. On the navigation pane, choose **Tasks**, and then choose the task that you want to edit\.

1. For **Actions**, choose **Edit** to open the **Edit tasks** page and expand **Schedule \(optional\)**\. 

1. In the **Schedule \(optional\)** section, configure your task to run on a schedule that you specify\.

1. For **Frequency**, configure how frequently you want the task to run, with a minimum interval of 1 hour\. For frequency configurations options, see [Configuring a task schedule](#configure-task-schedule)\.