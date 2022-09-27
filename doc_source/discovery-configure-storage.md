# Adding your on\-premises storage system to DataSync Discovery<a name="discovery-configure-storage"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

Specify an on\-premises storage system that you want AWS DataSync Discovery to collect information about and provide AWS storage migration recommendations for\.

## Providing access to your on\-premises storage system<a name="discovery-configure-storage-access"></a>

DataSync Discovery uses the credentials for your storage system's management interface to collect information about your storage\.

You must store these credentials in AWS Secrets Manager\. The secret must also be encrypted with a customer managed AWS Key Management Service \(AWS KMS\) key\. You can't use an AWS managed key for this secret\.

### Creating your AWS KMS key<a name="discovery-create-key"></a>

Configure the customer managed key in the same AWS Region where you're using DataSync\.

**To create an AWS KMS key**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. In the left navigation pane, choose **Customer managed keys**\.

1. Choose **Create key**\.

1. For **Key type**, choose **Symmetric**\. For **Key usage**, choose **Encrypt and decrypt**\.

1. Expand **Advanced options**, and do the following:

   1. For **Key material origin**, choose **KMS**\.

   1. For **Regionality**, choose **Single\-Region key**\.

1. Choose **Next**\.

1. Give your key an alias \(or name\), and choose **Next**\.

1. Assign yourself as a key administrator, and choose **Next**\.

1. Choose **Next** again, then choose **Finish** to create your key\.

1. Choose the key that you just created\.

1. Edit the **Key policy** to add a statement that allows DataSync to use the key\.

   1. Choose **Switch to policy view**, then **Edit**, and paste the following statement into the key policy editor:

      ```
      {
          "Effect": "Allow",
          "Principal": {
              "Service": "discovery-datasync.amazonaws.com"
          },
          "Action": [
              "kms:Decrypt",
              "kms:DescribeKey"
          ],
          "Resource": "arn:aws:kms:us-east-1:your-account-id:key/your-key-id"
      }
      ```

   1. Replace `your-account-id` with your AWS account number\.

   1. Replace `your-key-id` with the resource ID of the key that you just created\.

      You can find this ID in the Amazon Resource Name \(ARN\) that's on the same page in the console\.

   1. Choose **Save changes**\.

### Creating your secret<a name="discovery-create-secret"></a>

Configure a secret that's encrypted with the AWS KMS key that you just created\.

**To create a secret**

1. Open the AWS Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. In the left navigation pane, choose **Secrets**\.

1. Choose **Store a new secret**\.

1. Choose **Other type of secret**\.

1. For **Key/value pairs**, enter the following keys and provide corresponding values specific to your storage system:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/discovery-configure-storage.html)

1. For **Encryption key**, choose the AWS KMS key that you just created\. Choose **Next**\.

1. Give your secret a name, and choose **Next**\.

1. Choose **Next** to skip **Configure rotation**\.

1. Choose **Store** to create your secret\.

1. Refresh the page, and then choose the secret that you just created\.

1. For **Resource permissions \- optional**, choose **Edit permissions** and do the following:

   1. Copy and paste the following policy into the policy editor:

      ```
      {
          "Version": "2012-10-17",
          "Statement": [{
              "Effect": "Allow",
              "Principal": {
                  "Service": "discovery-datasync.amazonaws.com"
              },
              "Action": ["secretsmanager:GetSecretValue"],
              "Resource": "arn:aws:secretsmanager:us-east-1:your-account-id:secret:your-secret-id",
              "Condition": {
                  "StringEquals": {
                      "aws:SourceAccount": "your-account-id"
                  },
                  "ArnLike": {
                      "aws:SourceArn": "arn:aws:datasync:us-east-1:your-account-id:system/*"
                  }
              }
          }]
      }
      ```

   1. Replace `your-account-id` with your AWS account number\.

   1. Replace `your-secret-id` with the resource ID of the secret that you just created\.

      You can find this ID in the ARN that's on the same page in the console\.

1. Choose **Save**\.

## Adding your on\-premises storage system<a name="discovery-add-storage"></a>

You must provide some information about your storage system before DataSync Discovery can collect information about it\.

### Using the DataSync console<a name="discovery-add-storage-console"></a>

In the console, configure DataSync Discovery to work with your on\-premises storage system\.

**To add an on\-premises storage system by using the console**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Discovery**, and then choose **Add storage system**\.

1. For **Storage type**, choose the type of storage system that you're adding\.

1. For **Storage name**, enter a familiar name for your storage system\.

1. For **Management server**, enter the domain name or IP address of your storage system's management interface\.

1. For **Server port**, enter the network port that's needed to access the storage system's management interface\.

1. For **Secret**, choose an existing secret, or choose **Create a new secret** for your storage system's management interface credentials\.

   If you need to create a secret, see [Providing access to your on\-premises storage system](#discovery-configure-storage-access)\.

1. For **Agents**, do one of the following:
   + Choose the DataSync agent that you want to connect to your storage system's management interface\.
   + If you haven't created an agent, choose **Deploy a new DataSync agent**\. After your agent is up and running, you can finish adding your storage system\.

1. \(Optional\) Choose **Enable logging**\. Choose an existing Amazon CloudWatch log group or create a new one\.

   We recommend that you enable logging in case you need to troubleshoot the discovery job that's collecting information about your storage system\. For more information, see [Logging DataSync Discovery activity to CloudWatch](#discovery-enable-cloudwatch)\.

1. \(Optional\) Choose **Add tag** to tag the DataSync resource that represents your storage system\.

   *Tags* are key\-value pairs that help you manage, filter, and search for your DataSync resources\.

1. Choose **Add storage system**\.

### Using the AWS CLI<a name="discovery-add-storage-cli"></a>

Using the AWS Command Line Interface \(AWS CLI\), configure DataSync Discovery to work with your on\-premises storage system\.

**Note**  
The following instructions use the `datasync-discovery` command, but you can name this command something else\. For more information, see [Setting up the AWS CLI for DataSync Discovery](discovery-api-ref.md#discovery-api-cli-setup)\.

**Before you begin**
+ [Create a secret](#discovery-create-secret) that can access your on\-premises storage system's management interface\.
+ \(Recommended\) [Enable logging with CloudWatch](#discovery-enable-cloudwatch)\.

**To add an on\-premises storage system by using the AWS CLI**

1. Copy the following `add-storage-system` command:

   ```
   aws datasync-discovery add-storage-system \
     --server-configuration ServerHostname="domain-or-ip",ServerPort=network-port \
     --system-type storage-system-type \
     --agent-arns "agent-arn" \
     --secrets-manager-arn "secret-arn"
   ```

1. Specify the following required parameters in the command:
   + `--server-configuration ServerHostname` – Specify the domain name or IP address of your storage system's management interface\.
   + `--server-configuration ServerPort` – Specify the network port that's needed to connect with the system's management interface\.
   + `--system-type` – Specify the type of storage system that you're adding\.
   + `--agent-arns` – Specify the DataSync agent that you want to connect to your storage system's management interface\.

1. \(Optional\) Add any of the following parameters to the command:
   + `--cloud-watch-log-group-arn` – Specify the Amazon Resource Name \(ARN\) of the CloudWatch log group that you want to use to log DataSync Discovery activity\.
   + `--tags` – Specify a `Key` and `Value` to tag the DataSync resource that's representing your storage system\.

     A *tag* is a key\-value pair that helps you manage, filter, and search for your DataSync resources\.
   + `--name` – Specify a name for your storage system\.

1. Run the `add-storage-system` command\.

   You get a response that shows you the storage system ARN that you just added\.

   ```
   {
       "StorageSystemArn": "arn:aws:datasync:us-east-1:123456789012:system/storage-system-abcdef01234567890"
   }
   ```

After you add the storage system, you can run a discovery job to collect information about the storage system\.

## Removing your on\-premises storage system<a name="discovery-remove-storage"></a>

When you remove an on\-premises storage system from DataSync Discovery, you permanently delete any associated discovery jobs, collected data, and recommendations\.

### Using the DataSync console<a name="discovery-remove-storage-console"></a>

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Discovery**, and then choose the storage system that you want to remove\.

1. Choose **Actions**, then **Remove**\.

1. Enter **remove**, then choose **Remove**\.

### Using the AWS CLI<a name="discovery-remove-storage-cli"></a>

**Note**  
The following instructions use the `datasync-discovery` command, but you can name this command something else\. For more information, see [Setting up the AWS CLI for DataSync Discovery](discovery-api-ref.md#discovery-api-cli-setup)\.

1. Copy the following `remove-storage-system` command:

   ```
   aws datasync-discovery remove-storage-system --storage-system-arn "your-storage-system-arn"
   ```

1. For `--storage-system-arn`, specify the ARN of your storage system\.

1. Run the `remove-storage-system` command\.

   If successful, you get an HTTP 200 response with an empty HTTP body\.

## Logging DataSync Discovery activity to CloudWatch<a name="discovery-enable-cloudwatch"></a>

When you enable logging with CloudWatch, you can more easily troubleshoot issues with DataSync Discovery\. For example, if your discovery job is interrupted, you can check the logs to locate the issue\. If you resolve the problem within 12 hours of when it occurred, your discovery job picks up where it left off\.

If you add your on\-premises storage system using the console, DataSync can automatically enable logging for you\.

If you configure your system by using the AWS CLI, you must [create a log group](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) with a resource policy that allows DataSync to log events to the log group\. You can use a [log group resource policy](monitor-datasync.md#cloudwatchlogs) similar to one for DataSync tasks, with some differences:
+ For the service principal, use `discovery-datasync.amazonaws.com`\.
+ If you're using the `ArnLike` condition, specify a storage system ARN like this:

  ```
  "ArnLike": {
    "aws:SourceArn": [
      "arn:aws:datasync:region:account-id:system/*"
     ]
  },
  ```