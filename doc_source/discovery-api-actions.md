# AWS DataSync Discovery API operations<a name="discovery-api-actions"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

The following operations are supported with the DataSync Discovery API\.

**Topics**
+ [AddStorageSystem](#discovery-addstoragesystem)
+ [DescribeDiscoveryJob](#discovery-describediscoveryjob)
+ [DescribeStorageSystem](#discovery-describestoragesystem)
+ [DescribeStorageSystemResourceMetrics](#discovery-describestoragesystemresourcemetrics)
+ [DescribeStorageSystemResources](#discovery-describestoragesystemresources)
+ [GenerateRecommendations](#discovery-generaterecommendations)
+ [ListDiscoveryJobs](#discovery-listdiscoveryjobs)
+ [ListStorageSystems](#discovery-liststoragesystems)
+ [RemoveStorageSystem](#discovery-removestoragesystem)
+ [StartDiscoveryJob](#discovery-startdiscoveryjob)
+ [StopDiscoveryJob](#discovery-stopdiscoveryjob)
+ [UpdateDiscoveryJob](#discovery-updatediscoveryjob)
+ [UpdateStorageSystem](#discovery-updatestoragesystem)

## AddStorageSystem<a name="discovery-addstoragesystem"></a>

Creates a resource for an on\-premises storage system that you want DataSync Discovery to collect information about\.

### Request syntax<a name="discovery-addstoragesystem-request"></a>

```
{
   "AgentArns": [ "string" ],
   "ClientToken": "string",
   "CloudWatchLogGroupArn": "string",
   "Name": "string",
   "SecretsManagerArn": "string",
   "ServerConfiguration": { 
      "ServerHostname": "string",
      "ServerPort": number
   },
   "SystemType": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

### Request parameters<a name="discovery-addstoragesystem-request-params"></a>

**AgentArns**  
Specifies the Amazon Resource Name \(ARN\) of the DataSync agent that connects to and reads from your on\-premises storage system's management interface\.  
Type: Array of strings  
Array members: Fixed number of 1 item\.  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`  
Required: Yes

**ClientToken**  
Specifies a client token to make sure requests with this API operation are idempotent\. If you don't specify a client token, DataSync generates one for you automatically\.  
Type: String  
Pattern: `[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}`  
Required: Yes

**SecretsManagerArn**  
Specifies the ARN of a secret stored by AWS Secrets Manager\. DataSync Discovery uses this secret to access the management interface of your on\-premises storage system\. For information about creating a secret, see [Providing access to your on\-premises storage system](discovery-configure-storage.md#discovery-configure-storage-access)\.  
Type: String  
Length constraints: 2048  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):secretsmanager:[a-z\\-0-9]+:[0-9]{12}:secret:.*`  
Required: Yes

**ServerConfiguration**  
Specifies the server name and network port required to connect with the management interface of your on\-premises storage system\.  
Type: [DiscoveryServerConfiguration](discovery-api-data-types.md#DiscoveryServerConfiguration) object  
Required: Yes

**SystemType**  
Specifies the type of on\-premises storage system that you want DataSync Discovery to analyze\.  
DataSync Discovery currently supports NetApp Fabric\-Attached Storage \(FAS\) and All Flash FAS \(AFF\) systems running ONTAP 9\.8 or later\. 
Type: String  
Valid values: `NetAppONTAP`  
Required: Yes

**CloudWatchLogGroupArn**  
Specifies the ARN of the Amazon CloudWatch log group that's used to monitor and log discovery job events\.  
Type: String  
Length constraints: Maximum length of 562\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):logs:[a-z\-0-9]+:[0-9]{12}:log-group:([^:\*]*)(:\*)?$`  
Required: No

**Tags**  
Specifies labels that help you categorize, filter, and search for your AWS resources\. We recommend creating at least a name tag for your on\-premises storage system\.  
Type: Array of [TagListEntry](https://docs.aws.amazon.com/datasync/latest/userguide/API_TaskListEntry.html) objects  
Array members: Minimum number of 0 items\. Maximum number of 50 items\.  
Required: No

**Name**  
Specifies a familiar name for your on\-premises storage system\.  
Type: String  
Length constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`  
Required: No

### Response syntax<a name="discovery-addstoragesystem-response-syntax"></a>

```
{
   "StorageSystemArn": "string"
}
```

### Response elements<a name="discovery-addstoragesystem-response-elements"></a>

**StorageSystemArn**  
The ARN of the on\-premises storage system that you added to DataSync Discovery\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`

### Errors<a name="discovery-addstoragesystem-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## DescribeDiscoveryJob<a name="discovery-describediscoveryjob"></a>

Returns information about a DataSync discovery job\.

### Request syntax<a name="discovery-describediscoveryjob-request-syntax"></a>

```
{
   "DiscoveryJobArn": "string"
}
```

### Request parameters<a name="discovery-describediscoveryjob-request-params"></a>

**DiscoveryJobArn**  
Specifies the Amazon Resource Name \(ARN\) of the discovery job that you want information about\.  
Type: String  
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

### Response syntax<a name="discovery-describediscoveryjob-response-syntax"></a>

```
{
   "CollectionDurationMinutes": number,
   "DiscoveryJobArn": "string",
   "JobEndTime": number,
   "JobStartTime": number,
   "RecommendationStatus": "string",
   "Status": "string",
   "StorageSystemArn": "string"
}
```

### Response elements<a name="discovery-describediscoveryjob-response-elements"></a>

**CollectionDurationMinutes**  
The number of minutes that the discovery job runs\.  
Type: Integer  
Length constraints: Minimum value of 60\. Maximum value of 44640\.

**DiscoveryJobArn**  
The ARN of the discovery job\.  
Type: String  
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`

**JobEndTime**  
The time when the discovery job ended\.  
Type: Timestamp

**JobStartTime**  
The time when the discovery job started\.  
Type: Timestamp

**RecommendationStatus**  
Indicates whether DataSync Discovery can generate recommendations from data collected by a discovery job\. For more information, see [Recommendation statuses](discovery-job-statuses.md#recommendation-statuses-table)\.  
Type: String  
Valid values: `NONE | IN_PROGRESS | COMPLETED | COMPLETED_WITH_ERROR | FAILED`

**Status**  
Indicates the status of a discovery job\. For more information, see [Discovery job statuses](discovery-job-statuses.md#discovery-job-statuses-table)\.  
Type: String  
Valid values: `RUNNING | ERROR | TERMINATED | FAILED | STOPPED | COMPLETED | COMPLETED_WITH_ERROR`

**StorageSystemArn**  
The ARN of your on\-premises storage system\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`

### Errors<a name="discovery-describediscoveryjob-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## DescribeStorageSystem<a name="discovery-describestoragesystem"></a>

Returns information about an on\-premises storage system that you're using with DataSync Discovery\.

### Request syntax<a name="discovery-describestoragesystem-request-syntax"></a>

```
{
   "StorageSystemArn": "string"
}
```

### Request parameters<a name="discovery-describestoragesystem-request-params"></a>

**StorageSystemArn**  
Specifies the Amazon Resource Name \(ARN\) of an on\-premises storage system that you're using with DataSync Discovery\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

### Response syntax<a name="discovery-describestoragesystem-response-syntax"></a>

```
{
   "AgentArns": [ "string" ],
   "CloudWatchLogGroupArn": "string",
   "ConnectivityStatus": "string",
   "ErrorMessage": "string",
   "Name": "string",
   "SecretsManagerArn": "string",
   "ServerConfiguration": { 
      "ServerHostname": "string",
      "ServerPort": number
   },
   "StorageSystemArn": "string",
   "SystemType": "string"
}
```

### Response elements<a name="discovery-describestoragesystem-response-elements"></a>

**AgentArns**  
The ARN of the DataSync agent that connects to and reads from your on\-premises storage system\.  
Type: Array of strings  
Array members: Fixed number of 1 item\.  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`

**CloudWatchLogGroupArn**  
The ARN of the Amazon CloudWatch log group that's used to monitor and log discovery job events\.  
Type: String  
Length constraints: Maximum length of 562\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):logs:[a-z\-0-9]+:[0-9]{12}:log-group:([^:\*]*)(:\*)?$`

**ConnectivityStatus**  
Indicates whether your DataSync agent can access your on\-premises storage system\.  
Type: String  
Valid values: `PASS | FAIL | UNKNOWN`

**ErrorMessage**  
Describes the connectivity error that the DataSync agent is encountering with your on\-premises storage system\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `.*`

**SecretsManagerArn**  
The ARN of a secret stored by AWS Secrets Manager\. DataSync Discovery uses this secret to access the management interface of your on\-premises storage system\. For information about creating a secret, see [Providing access to your on\-premises storage system](discovery-configure-storage.md#discovery-configure-storage-access)\.  
Type: String  
Length constraints: 2048  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):secretsmanager:[a-z\\-0-9]+:[0-9]{12}:secret:.*`

**ServerConfiguration**  
The server name and network port required to connect with your on\-premises storage system's management interface\.  
Type: [DiscoveryServerConfiguration](discovery-api-data-types.md#DiscoveryServerConfiguration) object

**SystemType**  
The type of on\-premises storage system\.  
DataSync Discovery currently only supports NetApp Fabric\-Attached Storage \(FAS\) and All Flash FAS \(AFF\) systems running ONTAP 9\.8 or later\. 
Type: String  
Valid values: `NetAppONTAP`

### Errors<a name="discovery-describestoragesystem-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## DescribeStorageSystemResourceMetrics<a name="discovery-describestoragesystemresourcemetrics"></a>

Returns information, including performance data and capacity usage, which DataSync Discovery collects about a specific on\-premises storage system resource\.

### Request syntax<a name="discovery-describestoragesystemresourcemetrics-request-syntax"></a>

```
{
   "DiscoveryJobArn": "string",
   "EndTime": number,
   "MaxResults": number,
   "NextToken": "string",
   "ResourceId": "string",
   "ResourceType": "string",
   "StartTime": number
}
```

### Request parameters<a name="discovery-describestoragesystemresourcemetrics-request-params"></a>

**DiscoveryJobArn**  
Specifies the Amazon Resource Name \(ARN\) of the discovery job that's collecting information from your on\-premises storage system\.  
Type: String  
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

**ResourceId**  
Specifies the identifier of the storage system resource that you want information about\.  
Type: String  
Pattern: `[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}`  
Required: Yes

**ResourceType**  
Specifies what kind of storage system resource that you want returned\.  
Type: String  
Valid values: `VOLUME`   
Required: Yes

**EndTime**  
Specifies a time within the total duration that the discovery job ran\. To see information gathered during a certain time frame, use this parameter with `StartTime`\.  
Type: Timestamp  
Required: No

**MaxResults**  
Specifies how many results that you want in the response\.  
Type: Integer  
Valid range: Minimum value of 1\. Maximum value of 100\.  
Required: No

**NextToken**  
Specifies an opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`  
Required: No

**StartTime**  
Specifies a time within the total duration that the discovery job ran\. To see information gathered during a certain time frame, use this parameter with `EndTime`\.  
Type: Timestamp  
Required: No

### Response syntax<a name="discovery-describestoragesystemresourcemetrics-response-syntax"></a>

```
{
   "Metrics": [ 
      { 
         "Capacity": {
            "LogicalUsed": number,
            "Provisioned": number,
            "Used": number
         },
         "P95Metrics": { 
            "IOPS": { 
               "Other": number,
               "Read": number,
               "Total": number,
               "Write": number
            },
            "Latency": { 
               "Other": number,
               "Read": number,
               "Write": number
            },
            "Throughput": { 
               "Other": number,
               "Read": number,
               "Total": number,
               "Write": number
            }
         },
         "Timestamp": number
      }
   ],
   "NextToken": "string",
   "ResourceId": "string",
   "ResourceType": "string"
}
```

### Response elements<a name="discovery-describestoragesystemresourcemetrics-response-elements"></a>

**Metrics**  
The details about your storage system resource that were collected by DataSync Discovery\.  
Type: Array of [ResourceMetrics](discovery-api-data-types.md#discovery-api-resource-metrics) objects

**NextToken**  
The opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`

**ResourceId**  
The identifier of the storage system resource that you want information about\.  
Type: String  
Pattern: `[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}`

**ResourceType**  
The kind of storage system resource that you want returned\.  
Type: String  
Valid values: `VOLUME`

### Errors<a name="discovery-describestoragesystemresourcemetrics-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## DescribeStorageSystemResources<a name="discovery-describestoragesystemresources"></a>

Returns information collected by a discovery job about resources on your on\-premises storage system\.

### Request syntax<a name="discovery-describestoragesystemresources-request-syntax"></a>

```
{
   "DiscoveryJobArn": "string",
   "Filter": { 
      "string" : [ "string" ]
   },
   "MaxResults": number,
   "NextToken": "string",
   "ResourceIds": [ "string" ],
   "ResourceType": "string"
}
```

### Request parameters<a name="discovery-describestoragesystemresources-request-params"></a>

**DiscoveryJobArn**  
Specifies the Amazon Resource Name \(ARN\) of the discovery job that's collecting data from your on\-premises storage system\.  
Type: String  
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

**ResourceType**  
Specifies what kind of storage system resources that you want to be returned\.  
Type: String  
Valid values: `SVM | VOLUME`  
Required: Yes

**Filter**  
Filters the storage system resources that you want to be returned\. For example, this might be volumes associated with a specific storage virtual machine \(SVM\)\.  
Type: String to array of strings map  
Valid keys: `SVM`  
Length constraints: Maximum length of 1024\.  
Required: No

**MaxResults**  
Specifies the maximum number of storage system resources that you want to list\.  
Type: Integer  
Valid range: Minimum value of 1\. Maximum value of 100\.  
Required: No

**NextToken**  
Specifies an opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`  
Required: No

**ResourceIds**  
Specifies the identifiers of the storage system resources that you want information about\. You can't use this parameter in combination with the `Filter` parameter\.  
Type: Array of strings  
Pattern: `[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}`  
Required: No

### Response syntax<a name="discovery-describestoragesystemresources-response-syntax"></a>

```
{
   "NextToken": "string",
   "ResourceDetails": { array of storage system-specific objects }
}
```

### Response elements<a name="discovery-describestoragesystemresources-response-elements"></a>

**NextToken**  
The opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`

**ResourceDetails**  
The information collected about your storage system's resources\. This information can also include AWS storage service recommendations\. For more information, see [Storage resource information collected by AWS DataSync Discovery](discovery-understand-findings.md) and [Recommendations provided by AWS DataSync Discovery](discovery-understand-recommendations.md)\.  
Type: [ResourceDetails](discovery-api-data-types.md#ResourceDetails) object

### Errors<a name="discovery-describestoragesystemresources-response-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## GenerateRecommendations<a name="discovery-generaterecommendations"></a>

Creates recommendations about where to migrate your data to in AWS\. Recommendations are generated based on information that DataSync Discovery collects about your on\-premises storage system's resources\. For more information, see [Recommendations provided by AWS DataSync Discovery](discovery-understand-recommendations.md)\.

If your discovery job is completed successfully, you don't need to use this operation\. In this case, DataSync Discovery generates the recommendations for you automatically\.

### Request syntax<a name="discovery-generaterecommendations-request-syntax"></a>

```
{
   "DiscoveryJobArn": "string"
}
```

### Request parameters<a name="discovery-generaterecommendations-request-params"></a>

**DiscoveryJobArn**  
Specifies the Amazon Resource Name \(ARN\) of the discovery job that collected information about your on\-premises storage system\.  
Type: String  
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

### Response syntax<a name="discovery-generaterecommendations-response-syntax"></a>

```
{
   "RecommendationStatus": "string"
}
```

### Response elements<a name="discovery-generaterecommendations-response-elements"></a>

**RecommendationStatus**  
Indicates whether DataSync Discovery can provide recommendations\. For more information, see [Recommendation statuses](discovery-job-statuses.md#recommendation-statuses-table)\.  
Type: String  
Valid Values: `NONE | IN_PROGRESS | COMPLETED | COMPLETED_WITH_ERROR | FAILED`

### Errors<a name="discovery-generaterecommendations-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## ListDiscoveryJobs<a name="discovery-listdiscoveryjobs"></a>

Lists of all the existing DataSync discovery jobs that you have in the AWS Region and AWS account that you're using\.

### Request syntax<a name="discovery-listdiscoveryjobs-request-syntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string",
   "StorageSystemArn": "string"
}
```

### Request parameters<a name="discovery-listdiscoveryjobs-request-params"></a>

**MaxResults**  
Specifies how many results that you want in the response\.  
Type: Integer  
Valid range: Minimum value of 1\. Maximum value of 100\.  
Required: No

**NextToken**  
Specifies an opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`  
Required: No

**StorageSystemArn**  
Specifies the Amazon Resource Name \(ARN\) of an on\-premises storage system\. Include this parameter if you want to list only the discovery jobs that are associated with a specific storage system\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: No

### Response syntax<a name="discovery-listdiscoveryjobs-response-syntax"></a>

```
{
   "DiscoveryJobs": [ 
      { 
         "DiscoveryJobArn": "string",
         "Status": "string"
      }
   ],
   "NextToken": "string"
}
```

### Response elements<a name="discovery-listdiscoveryjobs-response-elements"></a>

**DiscoveryJobs**  
The discovery jobs that you've run\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`

**NextToken**  
The opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`

### Errors<a name="discovery-listdiscoveryjobs-response-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## ListStorageSystems<a name="discovery-liststoragesystems"></a>

Lists the on\-premises storage systems that you're using with DataSync Discovery\.

### Request syntax<a name="discovery-liststoragesystems-request-syntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

### Request parameters<a name="discovery-liststoragesystems-request-params"></a>

**MaxResults**  
Specifies how many results that you want in the response\.  
Type: Integer  
Valid range: Minimum value of 1\. Maximum value of 100\.  
Required: No

**NextToken**  
Specifies an opaque string that indicates the position to begin the next list of results in the response\.   
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`  
Required: No

### Response syntax<a name="discovery-liststoragesystems-response-syntax"></a>

```
{
   "NextToken": "string",
   "StorageSystems": [ 
      { 
         "StorageSystemArn": "string"
      }
   ]
}
```

### Response elements<a name="discovery-liststoragesystems-response-elements"></a>

**NextToken**  
The opaque string that indicates the position to begin the next list of results in the response\.  
Type: String  
Length constraints: Maximum length of 65535\.  
Pattern: `[a-zA-Z0-9=_-]+`

**StorageSystems**  
The ARNs of the on\-premises storage systems that you're using with DataSync Discovery\.  
Type: Array of [StorageSystemListEntry](discovery-api-data-types.md#discovery-api-storage-system-list-entry) objects

### Errors<a name="discovery-liststoragesystems-response-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## RemoveStorageSystem<a name="discovery-removestoragesystem"></a>

Permanently removes a storage system resource from DataSync Discovery, including the associated discovery jobs, collected data, and recommendations\.

### Request syntax<a name="discovery-removestoragesystem-request-syntax"></a>

```
{
   "StorageSystemArn": "string"
}
```

### Request parameters<a name="discovery-removestoragesystem-request-params"></a>

**StorageSystemArn**  
Specifies the Amazon Resource Name \(ARN\) of the storage system that you want to remove from DataSync Discovery\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

### Response elements<a name="discovery-removestoragesystem-response-elements"></a>

If the operation is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

### Errors<a name="discovery-removestoragesystem-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## StartDiscoveryJob<a name="discovery-startdiscoveryjob"></a>

Runs a DataSync discovery job on an on\-premises storage system\. If you haven't added the storage system yet, you must do so by using the [AddStorageSystem](#discovery-addstoragesystem) operation\.

### Request syntax<a name="discovery-startdiscoveryjob-request-syntax"></a>

```
{
   "ClientToken": "string",
   "CollectionDurationMinutes": number,
   "StorageSystemArn": "string"
}
```

### Request parameters<a name="discovery-startdiscoveryjob-request-params"></a>

**ClientToken**  
Specifies a client token to make sure requests with this API operation are idempotent\. If you don't specify a client token, DataSync generates one for you automatically\.  
Type: String  
Pattern: `[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}`   
Required: Yes

**CollectionDurationMinutes**  
Specifies in minutes how long that you want the DataSync discovery job to run\.  
Type: Integer  
Valid range: Minimum value of 60\. Maximum value of 44640\.  
Required: Yes

**StorageSystemArn**  
Specifies the Amazon Resource Name \(ARN\) of the on\-premises storage system that you want to run the discovery job on\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$ `  
Required: Yes

### Response syntax<a name="discovery-startdiscoveryjob-response-syntax"></a>

```
{
   "DiscoveryJobArn": "string"
}
```

### Response elements<a name="discovery-startdiscoveryjob-response-elements"></a>

**DiscoveryJobArn**  
The ARN of the discovery job that you started\.  
Type: String  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`

### Errors<a name="discovery-startdiscoveryjob-response-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## StopDiscoveryJob<a name="discovery-stopdiscoveryjob"></a>

Stops a DataSync discovery job that's running\. You can stop a discovery job anytime\. A job that's stopped before it's scheduled to end likely will provide you some information about your storage system resources\. To get recommendations for a stopped job, you must use the [GenerateRecommendations](#discovery-generaterecommendations) operation\.

### Request syntax<a name="discovery-stopdiscoveryjob-request-syntax"></a>

```
{
   "DiscoveryJobArn": "string"
}
```

### Request parameters<a name="discovery-stopdiscoveryjob-request-params"></a>

**DiscoveryJobArn**  
Specifies the Amazon Resource Name \(ARN\) of the discovery job that you want to stop\.   
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

### Response elements<a name="discovery-stopdiscoveryjob-response-elements"></a>

If the operation is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

### Errors<a name="discovery-stopdiscoveryjob-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## UpdateDiscoveryJob<a name="discovery-updatediscoveryjob"></a>

Modifies the configuration of a DataSync discovery job\.

### Request syntax<a name="discovery-updatediscoveryjob-request-syntax"></a>

```
{
   "CollectionDurationMinutes": number,
   "DiscoveryJobArn": "string"
}
```

### Request parameters<a name="discovery-updatediscoveryjob-request-params"></a>

**CollectionDurationMinutes**  
Specifies in minutes how long that you want the DataSync discovery job to run\. \(You can't set this parameter to less than the number of minutes that the job has already run for\.\)  
Type: Integer  
Valid range: Minimum value of 60\. Maximum value of 44640\.  
Required: Yes

**DiscoveryJobArn**  
Specifies the Amazon Resource Name \(ARN\) of the discovery job that you want to update\.  
Type: String  
Length constraints: Maximum length of 256\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}/job/discovery-job-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`  
Required: Yes

### Response elements<a name="discovery-updatediscoveryjob-response-elements"></a>

If the operation is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

### Errors<a name="discovery-updatediscoveryjob-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400

## UpdateStorageSystem<a name="discovery-updatestoragesystem"></a>

Modifies some configurations of an on\-premises storage system resource that's used by DataSync Discovery\.

### Request syntax<a name="adiscovery-updatestoragesystem-request-syntax"></a>

```
{
   "AgentArns": [ "string" ],
   "CloudWatchLogGroupArn": "string",
   "Name": "string",
   "SecretsManagerArn": "string",
   "ServerConfiguration": { 
      "ServerHostname": "string",
      "ServerPort": number
   },
   "StorageSystemArn": "string"
}
```

### Request parameters<a name="discovery-updatestoragesystem-request-params"></a>

**AgentArns**  
Specifies the Amazon Resource Name \(ARN\) of the DataSync agent that connects to and reads from your on\-premises storage system\.  
Type: Array of strings  
Array members: Fixed number of 1 item\.  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:agent/agent-[0-9a-z]{17}$`  
Required: Yes

**CloudWatchLogGroupArn**  
Specifies the ARN of the Amazon CloudWatch log group that is used to monitor and log discovery job events\.  
Type: String  
Length constraints: Maximum length of 562\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):logs:[a-z\-0-9]+:[0-9]{12}:log-group:([^:\*]*)(:\*)?$`  
Required: No

**Name**  
Specifies a familiar name for your on\-premises storage system\.  
Type: String  
Length constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^[a-zA-Z0-9\s+=._:@/-]+$`  
Required: No

**SecretsManagerArn**  
Specifies the ARN of the secret stored by AWS Secrets Manager\. DataSync Discovery uses this secret to access your on\-premises storage system's management interface\.  
Type: String  
Length constraints: 2048  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):secretsmanager:[a-z\\-0-9]+:[0-9]{12}:secret:.*`  
Required: Yes

**ServerConfiguration**  
Specifies the server name and network port that's required to connect with your on\-premises storage system's management interface\.  
Type: [DiscoveryServerConfiguration](discovery-api-data-types.md#DiscoveryServerConfiguration) object  
Required: Yes

**StorageSystemArn**  
Specifies the ARN of the on\-premises storage system that you want reconfigure\.  
Length constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:system/storage-system-[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$`   
Required: Yes

### Response elements<a name="discovery-updatestoragesystem-response-elements"></a>

If the operation is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

### Errors<a name="discovery-updatestoragesystem-errors"></a>

For information about the errors that are common to all operations, see [Common Errors](https://docs.aws.amazon.com/datasync/latest/userguide/CommonErrors.html)\.

**InternalException**  
This exception is thrown when an error occurs in the DataSync service\.  
HTTP Status Code: 500

**InvalidRequestException**  
This exception is thrown when the client submits a malformed request\.  
HTTP Status Code: 400