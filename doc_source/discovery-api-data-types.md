# AWS DataSync Discovery API data types<a name="discovery-api-data-types"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

The following data types are supported with the DataSync Discovery API\.

**Topics**
+ [Capacity](#discovery-api-capacity)
+ [DiscoveryJobListEntry](#DiscoveryJobListEntry)
+ [DiscoveryServerConfiguration](#DiscoveryServerConfiguration)
+ [IOPS](#discovery-api-iops)
+ [Latency](#discovery-api-latency)
+ [MaxP95Performance](#discovery-api-maxp95performance)
+ [NetAppONTAPSVM](#NetAppONTAPSVM)
+ [NetAppONTAPVolume](#NetAppONTAPVolume)
+ [P95Metrics](#discovery-api-p95metrics)
+ [Recommendation](#discovery-api-recommendation)
+ [ResourceDetails](#ResourceDetails)
+ [ResourceMetrics](#discovery-api-resource-metrics)
+ [StorageSystemListEntry](#discovery-api-storage-system-list-entry)
+ [Throughput](#discovery-api-throughput)

## Capacity<a name="discovery-api-capacity"></a>

The storage capacity of an on\-premises storage system resource \(for example, a storage virtual machine \[SVM\] or volume\)\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `LogicalUsed`  |  Long  |  The amount of space that's being used in a storage system resource without accounting for compression or deduplication\.  | 
|  `Provisioned`  |  Long  |  The total amount of space available in a storage system resource\.  | 
|  `Used`  |  Long  |  The amount of space that's being used in a storage system resource\.  | 

## DiscoveryJobListEntry<a name="DiscoveryJobListEntry"></a>

The details about a specific discovery job\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  ` DiscoveryJobArn `  |  String  |  The Amazon Resource Name \(ARN\) of a DataSync discovery job\.  | 
|  `Status`  |  String  |  The status of a discovery job\. For more information, see [Discovery job statuses](discovery-job-statuses.md#discovery-job-statuses-table)\.  | 

## DiscoveryServerConfiguration<a name="DiscoveryServerConfiguration"></a>

The settings that DataSync Discovery uses to connect with an on\-premises storage system's management interface\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `ServerHostname`  |  String  |  The domain name or IP address of your storage system's management interface\.  | 
|  `ServerPort`  |  String  |  The network port that's needed to access the system's management interface\.  | 

## IOPS<a name="discovery-api-iops"></a>

The IOPS peaks for an on\-premises storage system volume\. Each data point represents the 95th percentile peak value during a 1\-hour interval\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `Other`  | Double |  Peak IOPS unrelated to read and write operations\.  | 
|  `Read`  |  Double  |  Peak IOPS related to read operations\.  | 
|  `Total`  |  Double  | Peak total IOPS on your on\-premises storage system resource\. | 
|  `Write`  |  Double  | Peak IOPS related to write operations\. | 

## Latency<a name="discovery-api-latency"></a>

The latency peaks for an on\-premises storage system volume\. Each data point represents the 95th percentile peak value during a 1\-hour interval\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `Other`  |  Double  |  Peak latency for operations unrelated to read and write operations\.  | 
|  `Read`  |  Double  |  Peak latency for read operations\.  | 
|  `Write`  |  Double  | Peak latency for write operations\. | 

## MaxP95Performance<a name="discovery-api-maxp95performance"></a>

The performance data that DataSync Discovery collects about an on\-premises storage system volume\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `IopsOther`  |  Double  |  See [IOPS](#discovery-api-iops)\.  | 
|  `IopsRead`  |  Double  |  See [IOPS](#discovery-api-iops)\.  | 
|  `IopsTotal`  | Double |  See [IOPS](#discovery-api-iops)\.  | 
|  `IopsWrite`  | Double |  See [IOPS](#discovery-api-iops)\.  | 
|  `LatencyOther`  | Double |  See [Latency](#discovery-api-latency)\.  | 
|  `LatencyRead`  | Double |  See [Latency](#discovery-api-latency)\.  | 
|  `LatencyWrite`  | Double |  See [Latency](#discovery-api-latency)\.  | 
|  `ThroughputOther`  | Double |  See [Throughput](#discovery-api-throughput)\.  | 
|  `ThroughputRead`  | Double |  See [Throughput](#discovery-api-throughput)\.  | 
|  `ThroughputTotal`  | Double |  See [Throughput](#discovery-api-throughput)\.  | 
|  `ThroughputWrite`  | Double | See [Throughput](#discovery-api-throughput)\. | 

## NetAppONTAPSVM<a name="NetAppONTAPSVM"></a>

The information that DataSync Discovery collects about an on\-premises storage system SVM\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `SvmName`  |  String  |  The name of a storage virtual machine \(SVM\) in your storage system\.  | 
|  `SvmUuid`  |  String  |  The universally unique identifier \(UUID\) of an SVM in your storage system\.  | 

## NetAppONTAPVolume<a name="NetAppONTAPVolume"></a>

The information that DataSync Discovery collects about an on\-premises storage system volume\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `CapacityProvisioned`  |  Long  |  The total storage capacity that's available in the volume\.  | 
|  `CapacityUsed`  |  Long  |  The storage capacity that's being used in the volume\.  | 
|  `CifsClientCount`  | Long |  The number of Common Internet File System protocol \(CIFS\) clients that are connected to the volume\.   | 
|  `EnabledProtocols`  | Array of strings |  The data\-transfer protocols that are enabled on the volume \(for example, Network File System \[NFS\]\)\.  | 
|  `LogicalCapacityUsed`  | Long |  The amount of space that's being used in a storage system resource without accounting for compression or deduplication\.  | 
|  `MaxP95Performance `  | Object |  See [MaxP95Performance](#discovery-api-maxp95performance)\.  | 
|  `NfsClientCount `  | Long |  The number of Network File System \(NFS\) clients that are connected to the volume\.  | 
|  `Recommendations`  | Object |  See [Recommendation](#discovery-api-recommendation)\.  | 
|  `SvmName`  | String |  The name of the SVM that's associated with the volume\.  | 
|  `SvmUuid`  | String |  The UUID of the SVM that's associated with the volume\.  | 
|  `VolumeName`  | String |  The name of the volume\.  | 
|  `VolumeUuid`  | String | The UUID of the volume\. | 

## P95Metrics<a name="discovery-api-p95metrics"></a>

The types of performance data that DataSync Discovery collects about an on\-premises storage system volume\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `IOPS`  | Object |  See [IOPS](#discovery-api-iops)\.  | 
|  `Latency`  |  Object  | See [Latency](#discovery-api-latency)\. | 
|  `Throughput`  | Object | See [Throughput](#discovery-api-throughput)\. | 

## Recommendation<a name="discovery-api-recommendation"></a>

The details about an AWS storage service recommended by DataSync Discovery\. For more information, see [Recommendations provided by AWS DataSync Discovery](discovery-understand-recommendations.md)\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `EstimatedMonthlyStorageCost`  |  String  |  The estimated monthly cost of a recommended AWS storage service listed with `StorageType`\.  | 
|  `StorageConfiguration`  |  String to string map  |  Information about how you might set up a recommended AWS storage service\.  | 
|  `StorageType`  | String | A recommended AWS storage service that you might want to migrate data to based on information that DataSync Discovery collected from an on\-premises storage system\. | 

## ResourceDetails<a name="ResourceDetails"></a>

The on\-premises storage system resources that DataSync Discovery collects information about\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `NetAppONTAPSVMs`  |  Array of objects  |  See [NetAppONTAPSVM](#NetAppONTAPSVM)\.  | 
|  `NetAppONTAPVolumes`  |  Array of objects  |  See [NetAppONTAPVolume](#NetAppONTAPVolume)\.  | 

## ResourceMetrics<a name="discovery-api-resource-metrics"></a>

The information, including performance data and capacity usage, which DataSync Discovery collects about a specific on\-premises storage system resource\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `Capacity`  |  Object  |  See [Capacity](#discovery-api-capacity)\.  | 
|  `P95Metrics`  |  Object  |  See [P95Metrics](#discovery-api-p95metrics)\.  | 
|  `Timestamp`  | Timestamp | Indicates when the resource information was provided by DataSync Discovery\. | 

## StorageSystemListEntry<a name="discovery-api-storage-system-list-entry"></a>

The ARNs of the on\-premises storage systems that you're using with DataSync Discovery\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `StorageSystemArn`  |  String  |  The ARN of an on\-premises storage system that you added to DataSync Discovery\.  | 

## Throughput<a name="discovery-api-throughput"></a>

The throughput peaks for an on\-premises storage system volume\. Each data point represents the 95th percentile peak value during a 1\-hour interval\.


| Property | Data type | Description | 
| --- | --- | --- | 
|  `Other`  | Double |  Peak throughput unrelated to read and write operations\.  | 
|  `Read`  |  Double  |  Peak throughput related to read operations\.  | 
|  `Total`  |  Double  | Peak total throughput on your on\-premises storage system resource\. | 
|  `Write`  |  Double  | Peak throughput related to write operations\. | 