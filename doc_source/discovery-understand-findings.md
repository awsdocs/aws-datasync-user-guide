# Storage resource information collected by AWS DataSync Discovery<a name="discovery-understand-findings"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

AWS DataSync Discovery collects information about your on\-premises storage system that can help you understand how its storage resources are configured, performing, and utilized\. DataSync Discovery also uses this information to generate recommendations for migrating your data to AWS\.

A discovery job can give you the following information about your storage system's resources \(such as its volumes\):
+ The total storage capacity
+ The capacity that's available and in use
+ The number of Network File System \(NFS\) and Common Internet File System \(CIFS\) clients
+ The IOPS
+ The volume configurations
**Note**  
DataSync Discovery currently won't indicate that your volume uses the Internet Small Computer Systems Interface \(iSCSI\) protocol even if it's configured to use that protocol\.
+ The volume throughput
+ The volume latency

## Viewing information collected about your storage system<a name="discovery-view-metrics"></a>

You can begin to see what kind of information DataSync Discovery is collecting about your on\-premises storage system shortly after you start a discovery job\.

You can view this information by using the following options:
+ **The DataSync console** – Get visualized data about all of the storage system resources that DataSync Discovery can collect information about, including utilization, capacity, and configuration data\. You can see an overview of your storage system's resources or focus on individual resources\.
+ **The [DescribeStorageSystemResources](discovery-api-actions.md#discovery-describestoragesystemresources) operation** – Get data about all of the storage system resources that DataSync Discovery can collect information about, including utilization, capacity, and configuration data\. 
+ ** The [DescribeStorageSystemResourceMetrics](discovery-api-actions.md#discovery-describestoragesystemresourcemetrics) operation** – Get performance and capacity information that DataSync Discovery can collect about a specific resource in your storage system\.

### Using the DataSync console<a name="discovery-view-metrics-console"></a>

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Discovery**, and then choose the storage system that DataSync Discovery is collecting information about\.

   In the **Volumes** panel, you can see basic metrics about your storage system's resources\.

1. Choose a resource to see more detailed information about it on the **Capacity and performance data** tab\.

   You can see graphs that tell you about resource capacity, IOPS peaks, and more\.

### Using the AWS CLI<a name="discovery-view-metrics-cli"></a>

The following steps show how to use the `DescribeStorageSystemResources` operation with the AWS CLI\.

**Note**  
The following instructions use the `datasync-discovery` command, but you can name this command something else\. For more information, see [Setting up the AWS CLI for DataSync Discovery](discovery-api-ref.md#discovery-api-cli-setup)\.

1. Copy the following `describe-storage-system-resources` command:

   ```
   aws datasync-discovery describe-storage-system-resources \
     --discovery-job-arn "your-discovery-job-arn" \
     --resource-type "svm-or-volume"
   ```

1. Specify the following parameters in the command:
   + `--discovery-job-arn` – Specify the Amazon Resource Name \(ARN\) of the [discovery job](discovery-job-create.md#discovery-job-start) that you ran\.
   + `--resource-type` – Specify one of the following values, depending on what kind of storage system resources you want information about:
     + `SVM`
     + `VOLUME`

1. \(Optional\) Specify the `--resource-ids` parameter with the IDs of the storage system resources that you want information about\.

1. Run the `describe-storage-system-resources` command\.

   The following example response returns information that a discovery job collected about two storage system volumes\.

   Note that the `Recommendations` elements for each volume are empty\. In this situation, you have to run the `generate-recommendations` command before the `describe-storage-system-resources` command\. For more information, see [Viewing recommendations](discovery-understand-recommendations.md#discovery-understand-recommendations-view)\.

   ```
   {
       "ResourceDetails": {
           "NetAppONTAPVolumes": [{
                   "VolumeName": "svm1_root",
                   "VolumeUuid": "81e2cfd0-0de4-11ed-ac91-1357c81f7672",
                   "EnabledProtocols": [
                       "NFS"
                   ],
                   "CifsClientCount": 0,
                   "NfsClientCount": 1,
                   "SvmUuid": "7aaf267d-0de4-11ed-a083-5d35b5c8e451",
                   "SvmName": "svm1",
                   "CapacityUsed": 868352,
                   "CapacityProvisioned": 1073741824,
                   "MaxP95Performance": {
                       "IopsRead": 251.0,
                       "IopsWrite": 44.0,
                       "IopsOther": 17.0,
                       "IopsTotal": 345.0,
                       "ThroughputRead": 2.06,
                       "ThroughputWrite": 0.88,
                       "ThroughputOther": 0.11,
                       "ThroughputTotal": 2.17,
                       "LatencyRead": 0.06,
                       "LatencyWrite": 0.07,
                       "LatencyOther": 0.13
                   },
                   "Recommendations": []
               },
               {
                   "VolumeName": "vol1",
                   "VolumeUuid": "c3d02a5f-0de4-11ed-a083-5d35b5c8e451",
                   "EnabledProtocols": [
                       "NFS"
                   ],
                   "CifsClientCount": 0,
                   "NfsClientCount": 1,
                   "SvmUuid": "7aaf267d-0de4-11ed-a083-5d35b5c8e451",
                   "SvmName": "svm1",
                   "CapacityUsed": 1426984960,
                   "CapacityProvisioned": 10737418240,
                   "MaxP95Performance": {
                       "IopsRead": 117.14999999999995,
                       "IopsWrite": 130.34999999999988,
                       "IopsOther": 0.0,
                       "IopsTotal": 151.0,
                       "ThroughputRead": 7700042.749999996,
                       "ThroughputWrite": 8552884.749999993,
                       "ThroughputOther": 0.0,
                       "ThroughputTotal": 9926519.0,
                       "LatencyRead": 367.04999999999995,
                       "LatencyWrite": 3422.8499999999995,
                       "LatencyOther": 817.3499999999999
                   },
                   "Recommendations": []
               }
           ]
       }
   }
   ```