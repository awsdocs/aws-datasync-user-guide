# Working with DataSync discovery jobs<a name="discovery-job-create"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

After you deploy your AWS DataSync agent and add your on\-premises storage system to DataSync Discovery, you can run discovery jobs to collect information about the system and get AWS migration recommendations\. 

## Starting a discovery job<a name="discovery-job-start"></a>

You can run a discovery job for up to 31 days\. A storage system can have only one active discovery job at a time\. The information that a discovery job collects is available for up to 60 days following the end of the job \(unless you remove the related storage system from DataSync Discovery before that\)\.

**Tip**  
DataSync Discovery can provide more accurate recommendations the longer your discovery job runs\.

### Using the DataSync console<a name="discovery-job-start-console"></a>

With the console, you can run a discovery job for as little as one day\.

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Discovery**, and then choose the storage system that you want to run the discovery job on\.

1. Choose **Actions**, then **Start**\.

1. For **Duration**, choose how long that you want the discovery job to run\.

1. Choose **Start discovery job**\.

### Using the AWS CLI<a name="discovery-job-start-cli"></a>

With the AWS Command Line Interface \(AWS CLI\), you can run a discovery job for as little as 1 hour\.

**Note**  
The following instructions use the `datasync-discovery` command, but you can name this command something else\. For more information, see [Setting up the AWS CLI for DataSync Discovery](discovery-api-ref.md#discovery-api-cli-setup)\.

1. Copy the following `start-discovery-job` command:

   ```
   aws datasync-discovery start-discovery-job \
     --storage-system-arn "your-storage-system-arn" \
     --collection-duration-minutes discovery-job-duration
   ```

1. Specify the following parameters in the command:
   + `--storage-system-arn` – Specify the Amazon Resource Name \(ARN\) of the [on\-premises storage system that you added](discovery-configure-storage.md#discovery-add-storage) to DataSync Discovery\.
   + `--collection-duration-minutes` – Specify how long that you want the discovery job to run in minutes\. Enter a value between `60` \(1 hour\) and `44640` \(31 days\)\.

1. Run the `start-discovery-job` command\.

   You get a response that shows the discovery job that you just started\.

   ```
   {
       "DiscoveryJobArn": "arn:aws:datasync:us-east-1:123456789012:system/storage-system-abcdef01234567890/job/discovery-job-12345678-90ab-cdef-0abc-021345abcdef6"
   }
   ```

Shortly after starting the discovery job, you can begin [looking at the information that the job collects](discovery-understand-findings.md#discovery-view-metrics) \(including storage system capacity and usage\)\.

## Stopping a discovery job<a name="discovery-job-stop"></a>

Stop a discovery job at any time\. You can still get recommendations for a stopped job, but you must [generate the report manually](discovery-understand-recommendations.md#discovery-understand-recommendations-view)\.

### Using the DataSync console<a name="discovery-job-stop-console"></a>

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Discovery**, and then choose the storage system that you're running a discovery job on\.

1. Choose **Actions**, then **Stop \(keep data\)**\.

### Using the AWS CLI<a name="discovery-job-stop-cli"></a>

**Note**  
The following instructions use the `datasync-discovery` command, but you can name this command something else\. For more information, see [Setting up the AWS CLI for DataSync Discovery](discovery-api-ref.md#discovery-api-cli-setup)\.

1. Copy the following `stop-discovery-job` command:

   ```
   aws datasync-discovery stop-discovery-job --discovery-job-arn "your-discovery-job-arn"
   ```

1. For `--discovery-job-arn`, specify the ARN of the discovery job that's currently running\.

1. Run the `stop-discovery-job` command\.

   If successful, you get an HTTP 200 response with an empty HTTP body\.