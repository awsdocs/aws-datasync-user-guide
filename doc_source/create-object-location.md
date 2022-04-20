# Creating a location for object storage<a name="create-object-location"></a>

When you use a location in a task, you configure it as the source or destination location\. 

Your object storage system must be compatible with Amazon S3 for the following API calls\.
+ `AbortMultipartUpload`
+ `DeleteObject`
+ `GetBucketLocation`
+ `GetObject`
+ `GetObjectTagging`
+ `HeadBucket`
+ `ListBucket`
+ `ListBucketMultipartUploads`
+ `ListMultipartUploadParts`
+ `PutObject`
+ `PutObjectTagging`

Your object storage system must also support [AWS Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/API/sig-v4-authenticating-requests.html) for authenticating requests\. AWS Signature Version 2 is deprecated, and AWS DataSync doesn't support it\.

**To create a self\-managed object storage location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the navigation pane, choose **Locations**\. The locations that you previously created appear in the list of locations\.

1. On the **Locations** page, choose **Create location**\.

1. For **Location type**, choose **Object storage**\. You configure this location as a source or destination later\.

1. For **Agents**, choose one or more agents that you want to use from the available agents\. The agent connects to your self\-managed object storage server and makes it easier to securely transfer data between the self\-managed object storage location and AWS\.

1. For **Server**, provide the domain name or IP address of the self\-managed object storage server\. 

1. For **Bucket name**, enter the name of the self\-managed object storage bucket that you will use for the data transfer\.

1. For **Folder**, enter an object prefix that will be used for the data transfer\. When your location is used as a source for a task, DataSync will only copy objects with the provided prefix\. When your location is used as a destination for a task, all objects will be written under the provided prefix\. 

1. To select the object storage server protocol and server port, choose **Additional settings**\. Select either **HTTP** or **HTTPS**\.

   By default, the **Server port** is set to **80** for HTTP, and **443** for HTTPS, but you can specify a custom port if your self\-managed object storage server requires one\.

1. \(Optional\) If credentials are required to access the self\-managed object storage location, select **Requires credentials**, and enter the **Access key** and the **Secret key** that are needed to access the bucket\. The access key and secret key parameters can also be used to provide user name and password, respectively\.

1. \(Optional\) **Tags** are key\-value pairs that help you manage, filter, and search for your location\. Adding a tag is optional\. We recommend using tags for naming your resources\. 

1. When you're done, choose **Create location**\.