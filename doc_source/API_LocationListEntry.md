# LocationListEntry<a name="API_LocationListEntry"></a>

Represents a single entry in a list of locations\. `LocationListEntry` returns an array that contains a list of locations when the [ListLocations](https://docs.aws.amazon.com/datasync/latest/userguide/API_ListLocations.html) operation is called\.

## Contents<a name="API_LocationListEntry_Contents"></a>

 ** LocationArn **   <a name="DataSync-Type-LocationListEntry-LocationArn"></a>
The Amazon Resource Name \(ARN\) of the location\. For Network File System \(NFS\) or Amazon EFS, the location is the export path\. For Amazon S3, the location is the prefix path that you want to mount and use as the root of the location\.  
Type: String  
Length Constraints: Maximum length of 128\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso|aws-iso-b):datasync:[a-z\-0-9]+:[0-9]{12}:location/loc-[0-9a-z]{17}$`   
Required: No

 ** LocationUri **   <a name="DataSync-Type-LocationListEntry-LocationUri"></a>
Represents a list of URIs of a location\. `LocationUri` returns an array that contains a list of locations when the [ListLocations](https://docs.aws.amazon.com/datasync/latest/userguide/API_ListLocations.html) operation is called\.  
Format: `TYPE://GLOBAL_ID/SUBDIR`\.  
TYPE designates the type of location \(for example, `nfs` or `s3`\)\.  
GLOBAL\_ID is the globally unique identifier of the resource that backs the location\. An example for EFS is `us-east-2.fs-abcd1234`\. An example for Amazon S3 is the bucket name, such as `myBucket`\. An example for NFS is a valid IPv4 address or a hostname that is compliant with Domain Name Service \(DNS\)\.  
SUBDIR is a valid file system path, delimited by forward slashes as is the \*nix convention\. For NFS and Amazon EFS, it's the export path to mount the location\. For Amazon S3, it's the prefix path that you mount to and treat as the root of the location\.  
  
Type: String  
Length Constraints: Maximum length of 4356\.  
Pattern: `^(efs|nfs|s3|smb|hdfs|fsx[a-z0-9]+)://[a-zA-Z0-9.:/\-]+$`   
Required: No

## See Also<a name="API_LocationListEntry_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/LocationListEntry) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/LocationListEntry) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/LocationListEntry) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/LocationListEntry) 