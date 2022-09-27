# AWS DataSync Discovery API Reference<a name="discovery-api-ref"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

Use the following API operations to configure and manage AWS DataSync Discovery\.

**Topics**
+ [Setting up the AWS CLI for DataSync Discovery](#discovery-api-cli-setup)
+ [AWS DataSync Discovery API operations](discovery-api-actions.md)
+ [AWS DataSync Discovery API data types](discovery-api-data-types.md)

## Setting up the AWS CLI for DataSync Discovery<a name="discovery-api-cli-setup"></a>

You can currently use DataSync Discovery API operations with the [AWS Command Line Interface \(AWS CLI\) version 2](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)\.

**To set up the AWS CLI for DataSync Discovery**

1. To download the DataSync Discovery service model, choose [api\-2\.zip](samples/api-2.zip)\.

1. Unzip the file\.

1. Run the following command to add the `api-2.json` model to your AWS CLI configuration\.

   This example creates a `datasync-discovery` service name\. You can specify a different name\.

   ```
   aws configure add-model --service-model file://api-2.json --service-name datasync-discovery
   ```

After you add the model, you can run DataSync Discovery commands \(for example, `aws datasync-discovery start-discovery-job`\)\.