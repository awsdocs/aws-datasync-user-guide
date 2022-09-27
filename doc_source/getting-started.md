# Getting started with AWS DataSync<a name="getting-started"></a>

In this topic, you can find step\-by\-step instructions on how to get started using AWS DataSync on the AWS Management Console\.

Before you begin, we recommend reading [How AWS DataSync works](how-datasync-works.md) to understand the components and terms used in DataSync and how DataSync works\. We also recommend reading the [Using identity\-based policies \(IAM policies\) for DataSync](using-identity-based-policies.md) section to understand the AWS Identity and Access Management \(IAM\) permissions that DataSync requires\.

**To use AWS DataSync**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the upper\-right corner, select the AWS Region where you want to run DataSync\.

   We recommend choosing the AWS Region where the AWS storage resource that's involved in your transfer resides\. For a list of AWS storage services that DataSync supports, see [Working with AWS DataSync locations](working-with-locations.md)\.

1. On the DataSync home page, choose whether to transfer data **Between on\-premises storage and AWS** or **Between AWS Storage services**\.

1. Choose **Get started** to begin using DataSync\. 

   If this is your first time using DataSync in this AWS Region, the **Create agent** page appears\. From this page, you can download your virtual machine \(VM\) or create an Amazon EC2 instance\. 

   If you have used DataSync in this AWS Region, the **Agents** page appears and you can see your agents listed\.

Next, take the following steps\.

**Topics**
+ [Create an AWS DataSync agent](configure-agent.md)
+ [Configure a source location](configure-source-location.md)
+ [Configure a destination location](create-destination-location.md)
+ [Configure task settings](create-task.md)
+ [Review your settings and create your task](review-settings.md)
+ [Start your task](run-your-task.md)
+ [Clean up resources](clean-up.md)