# Recommendations provided by AWS DataSync Discovery<a name="discovery-understand-recommendations"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

After DataSync Discovery collects information about your on\-premises storage system, it can recommend moving your data on a per\-volume basis to one or more of the following AWS storage services:
+ Amazon FSx for NetApp ONTAP
+ Amazon Elastic File System \(Amazon EFS\)
+ Amazon FSx for Windows File Server

## What's included in the recommendations?<a name="discovery-understand-recommendations-how"></a>

DataSync Discovery recommendations include storage configurations and cost estimates to help you choose the AWS storage service that works for your data\.

### AWS storage configuration<a name="discovery-understand-recommendations-storage-configs"></a>

DataSync Discovery provides information about how you might want to configure a recommended AWS storage service\. The storage configuration is designed to optimize costs while helping meet storage performance and capacity needs based on information that's collected during a discovery job\.

The storage configuration is only an approximation and might not account for all capabilities provided by an AWS storage service\. For more information, see [What's not included in the recommendations?](#discovery-understand-recommendations-how-not)

### Estimated cost<a name="discovery-understand-recommendations-estimated-cost"></a>

DataSync Discovery provides an estimated monthly cost for each AWS storage service that it recommends\. The cost is based on standard AWS pricing and provides only an estimate of your AWS fees\. It does not include any taxes that might apply\. Your actual fees depend on a variety of factors, including your usage of AWS services\.

The estimated cost also doesn't include the one\-time or periodic fees for migrating your data to AWS\.

## What's not included in the recommendations?<a name="discovery-understand-recommendations-how-not"></a>

The following AWS storage capabilities currently aren't accounted for when DataSync Discovery determines recommendations for you:
+ **Amazon FSx for NetApp ONTAP** – Single\-AZ deployments and backup storage
+ **Amazon EFS** – EFS One Zone storage classes and backup storage
+ **Amazon FSx for Windows File Server** – Single\-AZ deployments and backup storage

## Viewing recommendations<a name="discovery-understand-recommendations-view"></a>

You can view recommendations after your discovery job is completed successfully, when you stop the job, and even sometimes when the job is completed but had issues collecting information from your storage system\. Recommendations aren't available if your discovery job fails\. For more information, see [Discovery job statuses](discovery-job-statuses.md#discovery-job-statuses-table)\.

Recommendations can take up to 1 hour to generate after a discovery job is completed\. If your discovery job is completed successfully, DataSync Discovery generates the recommendations for you\. If you stop the job early, or the job is completed with issues, you must generate recommendations manually\.

**Tip**  
Before starting your migration to AWS, review the DataSync Discovery recommendations with your AWS account team\.

### Using the DataSync console<a name="view-recommendations-console"></a>

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Discovery**, and then choose the storage system that you ran your discovery job on\.

1. If your recommendations don't generate automatically, go to the **Discovery** panel and choose **Get recommendations**\.

1. After you see that recommendations are available, choose the resource that you want recommendations on\.

1. Choose **Recommendations and estimates** to see the recommendations for that resource\.

### Using the AWS CLI<a name="view-recommendations-cli"></a>

**Note**  
The following instructions use the `datasync-discovery` command, but you can name this command something else\. For more information, see [Setting up the AWS CLI for DataSync Discovery](discovery-api-ref.md#discovery-api-cli-setup)\.

1. Copy the following `describe-discovery-job` command:

   ```
   aws datasync-discovery describe-discovery-job --discovery-job-arn "your-discovery-job-arn"
   ```

1. For the `--discovery-job-arn` parameter, specify the Amazon Resource Name \(ARN\) of the [discovery job](discovery-job-create.md#discovery-job-start) that you ran on the storage system\.

1. Run the `describe-discovery-job` command\.

   If your response includes a `Status` that isn't `FAILED`, you can continue\. If you see `FAILED`, you must run another discovery job on your storage system to try to generate recommendations\.

1. If your discovery job is completed successfully, skip this step\. Otherwise, do the following to manually generate recommendations:

   1. Copy the following `generate-recommendations` command:

      ```
      aws datasync-discovery generate-recommendations --discovery-job-arn "your-discovery-job-arn"
      ```

   1. For the `--discovery-job-arn` parameter, specify the ARN of the same discovery job that you specified in Step 2\.

   1. Run the `generate-recommendations` command\.

   1. Wait until the `RecommendationStatus` element in the response has a `COMPLETED` status, then move to the next step\.

1. Copy the following `describe-storage-system-resources` command:

   ```
   aws datasync-discovery describe-storage-system-resources \
     --discovery-job-arn "your-discovery-job-arn" \
     --resource-type "VOLUME"
   ```

1. Specify the following parameters in the command:
   + `--discovery-job-arn` – Specify the ARN of the same discovery job that you specified in Step 2\.
   + `--resource-type` – Specify `VOLUME`\.

     This parameter returns recommendations for volumes in your storage system\.

1. Run the `describe-storage-system-resources` command\.

   In this example response, the `Recommendations` element suggests an AWS storage service where you can migrate a specific volume, how you might configure that service, and the estimated monthly AWS storage costs\.

   ```
   {
       "Recommendations": [{
           "StorageType": "fsxOntap",
           "StorageConfiguration": {
               "DeploymentType": "Multi-AZ",
               "ProvisionedIOpsMode": "User Provisioned",
               "StorageCapacityGB": "2940",
               "ThroughputCapacity": "2048",
               "TotalIOps": "65000"
           },
           "EstimatedMonthlyStorageCost": "5617.81"
       }]
   }
   ```