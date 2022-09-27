# Creating an object storage location<a name="create-object-location"></a>

A *location* is an endpoint for an object storage system, which can be hosted on\-premises or by another cloud provider \(for example, a Google Cloud Storage bucket\)\.

## Prerequisites<a name="create-object-location-prerequisites"></a>

Your object storage system must be compatible with the following [Amazon S3 API operations](https://docs.aws.amazon.com/AmazonS3/latest/API/API_Operations.html) for AWS DataSync to connect to it:
+ `AbortMultipartUpload`
+ `CompleteMultipartUpload`
+ `CopyObject`
+ `CreateMultipartUpload`
+ `DeleteObject`
+ `DeleteObjects`
+ `DeleteObjectTagging`
+ `GetBucketLocation`
+ `GetObject`
+ `GetObjectTagging`
+ `HeadBucket`
+ `HeadObject`
+ `ListObjectsV2`
+ `PutObject`
+ `PutObjectTagging`
+ `UploadPart`

Your object storage system must also support [AWS Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/API/sig-v4-authenticating-requests.html) for authenticating requests\. \(AWS Signature Version 2 is deprecated\.\)

## Considerations when migrating to or from a Google Cloud Storage bucket<a name="object-storage-considerations"></a>

Because DataSync communicates with Google Cloud Storage by using the Amazon S3 API, there's a limitation that might cause your DataSync task to fail if you try to copy object tags\. To prevent this, clear the **Copy object tags** check box when configuring your task settings\. For more information, see [File metadata and management options](create-task.md#configure-file)\.

For detailed instructions on migrating from Google Cloud Storage, see [Tutorial: Transferring data from Google Cloud Storage to Amazon S3](tutorial_transfer-google-cloud-storage.md)\.

## Creating the location<a name="create-object-location-how-to"></a>

Your object storage system can be a source or destination location for DataSync\.

**To create an object storage location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Locations**\.

1. On the **Locations** page, choose **Create location**\.

1. For **Location type**, choose **Object storage**\.

   You configure this location as a source or destination later\.

1. For **Agents**, choose one or more agents that you want to use\.

   During the transfer, the agent securely connects to your object storage server\.

1. For **Server**, provide the domain name or IP address of the object storage server\. 

1. For **Bucket name**, enter the name of the object storage bucket involved in the transfer\.

1. For **Folder**, enter an object prefix\.

   If this is a source location, DataSync only copies objects with this prefix\. If this is a destination location, DataSync writes all objects with this prefix\. 

1. To select the object storage server protocol and server port, choose **Additional settings** and select either **HTTP** or **HTTPS**\.

   By default, the **Server port** is set to **80** for HTTP and **443** for HTTPS\. You can specify a custom port if needed\.

1. \(Optional\) If credentials are required to access the object storage location, select **Requires credentials** and enter the **Access key** and **Secret key** for accessing the bucket\.

   You can also use the access key and secret key settings to provide a user name and password, respectively\.

1. \(Optional\) **Tags** are key\-value pairs that help you manage, filter, and search for your location\.

   We recommend using tags for naming your locations\. 

1. Choose **Create location**\.