# Using the AWS Command Line Interface with AWS DataSync<a name="using-cli"></a>

In this section, you can find examples of using the AWS Command Line Interface \(AWS CLI\) commands for AWS DataSync\. You can use these commands to create an agent, create source and destination locations, and run a task\.

Before you begin, we recommend reading [How AWS DataSync works](how-datasync-works.md) to understand the components and terms used in DataSync and how the service works\. We also recommend reading [Using identity\-based policies \(IAM policies\) for DataSync](using-identity-based-policies.md) to understand the AWS Identity and Access Management \(IAM\) permissions that DataSync requires\.

Before you use AWS CLI commands, install the AWS CLI\. For information about how to install the AWS CLI, see [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) in the *AWS Command Line Interface User Guide*\. After you install the AWS CLI, you can use the `help` command to see the DataSync operations and the parameters associated with them\. 

To see the available operations, enter the following command\.

`aws datasync help`

To see the parameters associated with a specific operation, enter the following command\.

`aws datasync operation help`

For more information about the AWS CLI, see [What is the AWS Command Line Interface?](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)

**Topics**
+ [Creating an agent](create-agent-cli.md)
+ [Creating locations](create-locations-cli.md)
+ [Creating a task](create-task-cli.md)
+ [Starting a task](start-task-execution.md)
+ [Monitoring your task](monitor-task-execution.md)
+ [API filters for ListTasks and ListLocations](query-resources.md)

For information about supported AWS Regions and endpoints, see [DataSync AWS Regions and endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#datasync-region)\.

For information about DataSync Amazon Resource Name \(ARN\) values, see [DataSync Amazon Resource Names](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html#arn-syntax-datasync)\.