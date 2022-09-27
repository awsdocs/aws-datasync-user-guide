# Filtering AWS DataSync resources<a name="query-resources"></a>

You can filter your AWS DataSync locations and tasks by using the `ListLocations` and `ListTasks` API operations in the AWS CLI\. For example, retrieve a list of your most recent tasks\.

## Parameters for filtering<a name="API-filter-parameters"></a>

You can use API filters to narrow down the list of resources returned by `ListTasks` and `ListLocations`\. For example, to retrieve all of your Amazon S3 locations, you can use `ListLocations` with the filter name `LocationType` *`S3`* and `Operator` *`Equals`*\.

To filter API results, you must specify a filter name, operator, and value\.
+ `Name` – The name of the filter that's being used\. Each API call supports a list of filters that are available for it \(for example, `LocationType` for `ListLocations`\)\.
+ `Values` – The values that you want to filter for\. For example, you might want to display only Amazon S3 locations\.
+ `Operator` – The operator that's used to compare filter values \(for example, `Equals` or `Contains`\)\. 

The following table lists the available operators\.


| Operator | Key types | 
| --- | --- | 
| Equals | String, Number | 
| NotEquals | String, Number | 
| LessThan | Number | 
| LessThanOrEqual | Number | 
| GreaterThan | Number | 
| GreaterThanOrEqual | Number | 
| In | String | 
| Contains | String | 
| NotContains | String | 
| BeginsWith | String | 

## Filtering by location<a name="ListLocations"></a>

`ListLocations` supports the following filter names:
+ `LocationType` – Filters on the location type:
  + `SMB`
  + `NFS`
  + `HDFS`
  + `OBJECT_STORAGE`
  + `S3`
  + `OUTPOST_S3`
  + `FSX_WINDOWS`
  + `FSX_LUSTRE`
  + `FSX_OPENZFS_NFS`
  + `FSX_ONTAP_NFS`
  + `FSX_ONTAP_SMB`
+ `LocationUri` – Filters on the uniform resource identifier \(URI\) assigned to the location, as returned by the `DescribeLocation*` API call \(for example, `s3://bucket-name/your-prefix` for Amazon S3 locations\)\.
+ `CreationTime` – Filters on the time that the location was created\. The input format is `yyyy-MM-dd:mm:ss` in Coordinated Universal Time \(UTC\)\.

The following AWS CLI example lists all locations of type Amazon S3 that have a location URI starting with the string `"s3://DOC-EXAMPLE-BUCKET"` and that were created at or after 2019\-12\-15 17:15:20 UTC\. 

```
aws datasync list-locations \
    --filters [{Name=LocationType, Values=["S3"], Operator=Equals}, {Name=LocationUri, Values=["s3://DOC-EXAMPLE-BUCKET"], Operator=BeginsWith}, {Name=CreationTime,Values=["2019-12-15 17:15:20"],Operator=GreaterThanOrEqual}]
```

This command returns output similar to the following\.

```
{
    "Locations": [
        {
            "LocationArn": "arn:aws:datasync:us-east-1:111122223333:location/loc-333333333abcdef0",
            "LocationUri": "s3://DOC-EXAMPLE-BUCKET-examples/"
        },
        {
            "LocationArn": "arn:aws:datasync:us-east-1:123456789012:location/loc-987654321abcdef0",
            "LocationUri": "s3://DOC-EXAMPLE-BUCKET-examples-2/"
        }
    ]
}
```

## Filtering by task<a name="ListTasks"></a>

`ListTasks` supports the following filter names\.
+ `LocationId` – Filters on both source and destination locations on Amazon Resource Name \(ARN\) values\.
+ `CreationTime` – Filters on the time that the task was created\. The input format is `yyyy-MM-dd:mm:ss` in UTC\.

The following AWS CLI example shows the syntax when filtering on `LocationId`\.

```
aws datasync list-tasks \
    --filters Name=LocationId,Values=arn:aws:datasync:us-east-1:your-account-id:location/your-location-id,Operator=Contains
```

The output of this command looks similar to the following\.

```
{
    "Tasks": [
        {
            "TaskArn": "arn:aws:datasync:us-east-1:your-account-id:task/your-task-id",
            "Status": "AVAILABLE",
            "Name": "DOC-EXAMPLE-BUCKET"
        }
    ]
}
```