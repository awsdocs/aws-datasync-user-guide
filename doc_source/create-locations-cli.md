# Creating AWS DataSync locations with the AWS CLI<a name="create-locations-cli"></a>

Each AWS DataSync task is made up of a pair of locations in a transfer\. The source location defines the storage system or service that you want to read data from\. The destination location defines the storage system or service that you want to write data to\.

With the AWS Command Line Interface \(AWS CLI\), you can create locations for the following storage systems and services:
+ Network File System \(NFS\)
+ Server Message Block \(SMB\)
+ Hadoop Distributed File System \(HDFS\)
+ Self\-managed object storage source locations
+ Amazon Elastic File System \(Amazon EFS\)
+ Amazon FSx for Windows File Server
+ Amazon FSx for Lustre
+ Amazon FSx for OpenZFS
+ Amazon FSx for NetApp ONTAP
+ Amazon Simple Storage Service \(Amazon S3\)

For more information, see [Working with AWS DataSync locations](working-with-locations.md)\.

## Creating an NFS location<a name="create-location-nfs-cli"></a>

An NFS location defines a file system on an NFS server that can be read from or written to\. You can also create an NFS location by using` the AWS Management Console\. For more information, see [Creating an NFS location](create-nfs-location.md)\. 

**Note**  
If you are using an NFS location on an AWS Snowcone device, see [NFS server on AWS Snowcone](create-nfs-location.md#nfs-on-snowcone) for more information about transferring data to or from that device\.

**To create an NFS location by using the CLI**
+ Use the following command to create an NFS source location\.

  ```
  $ aws datasync create-location-nfs \
      --server-hostname nfs-server-address \
      --on-prem-config AgentArns=datasync-agent-arns \
      --subdirectory nfs-export-path
  ```

  For the preceding command, the following applies:
  + The path \(`nfs-export-path`\) that you provide for the `--subdirectory` parameter must be a path that's exported by the NFS server, or a subdirectory\. Other NFS clients in your network must be able to mount this path\. To see all the paths exported by your NFS server, run the command `showmount -e nfs-server-address` from an NFS client with access to your server\. You can specify any directory that appears in the results, and any subdirectory of that directory\. 
  + To transfer all the data in the folder that you specified, DataSync needs permissions to read all the data\. To give DataSync permissions, you can do one of two things\. You can configure the NFS export with `no_root_squash`\. Or, for the all files that you want DataSync to access, you can make sure that the permissions allow read access for all users\. Doing either enables the agent to read the files\. For the agent to access directories, you must additionally give all users execute access\.
  + Make sure that the NFS export path is accessible without Kerberos authentication\.

  DataSync automatically chooses the NFS version that it uses to read from an NFS location\. To specify an NFS version, use the optional `Version` parameter in the [NfsMountOptions](API_NfsMountOptions.md) API operation\.

This command returns the Amazon Resource Name \(ARN\) of the NFS location, similar to the ARN shown following\.

`{ "LocationArn": "arn:aws:datasync:us-east-1:111222333444:location/loc-0f01451b140b2af49" }`

To make sure that the directory can be mounted, you can connect to any computer that has the same network configuration as your agent and run the following command\. 

```
mount -t nfs -o nfsvers=<nfs-server-version <nfs-server-address:<nfs-export-path <test-folder
```

The following is an example of the command\.

```
mount -t nfs -o nfsvers=3 198.51.100.123:/path_for_sync_to_read_from /temp_folder_to_test_mount_on_local_machine
```

## Creating an SMB location<a name="create-location-smb-cli"></a>

An SMB location defines a file system on an SMB server that can be read from or written to\. You can also create an SMB location by using the console\. For more information, see [Creating an SMB location](create-smb-location.md)\. 

**To create an SMB location by using the CLI**
+ Use the following command to create an SMB source location\.

  ```
  aws datasync create-location-smb \
      --server-hostname smb-server-address \
      --user user-who-can-mount-share \
      --domain domain-of-the-smb-server \
      --password user-password \
      --agent-arns datasync-agent-arns \
      --subdirectory smb-export-path
  ```

  The `smb-export-path` that you provide for the `--subdirectory` parameter should be a path that's exported by the SMB server, or a subdirectory\. Specify the path by using forward slashes; for example, `/path/to/folder`\. Other SMB clients in your network should be able to access this path\.

  DataSync automatically chooses the SMB version that it uses to read from an SMB location\. To specify an SMB version, use the optional `Version` parameter in the [SmbMountOptions](API_SmbMountOptions.md) API operation\.

This command returns the Amazon Resource Name \(ARN\) of the SMB location, similar to the ARN shown following\.

```
{ 
    "LocationArn": "arn:aws:datasync:us-east-1:111222333444:location/loc-0f01451b140b2af49" 
}
```

## Creating an HDFS location<a name="create-location-hdfs-cli"></a>

An HDFS location defines a file system on a Hadoop cluster that can be read from or written to\. You can also create an HDFS location by using the AWS Management Console\. For more information, see [Creating an HDFS location](create-hdfs-location.md)\.

**To create an HDFS location by using the AWS CLI**
+ Use the following command to create an HDFS location\. In the following example, replace each `user input placeholder` with your own information\.

  ```
  aws datasync create-location-hdfs --name-nodes [{"Hostname":"host1", "Port": 8020}] \
      --authentication-type "SIMPLE|KERBEROS" \
      --agent-arns [arn:aws:datasync:us-east-1:123456789012:agent/agent-01234567890example] \
      --subdirectory "/path/to/my/data"
  ```

  The following parameters are required in the `create-location-hdfs` command:
  + `name-nodes` – Specifies the hostname or IP address of the NameNode in the Hadoop cluster and the TCP port that the NameNode is listening on\.
  + `authentication-type` – The type of authentication to use when connecting to the Hadoop cluster\. Specify `SIMPLE` or `KERBEROS`\.

    If you use `SIMPLE` authentication, use the `--simple-user` parameter to specify the user name of the user\. If you use `KERBEROS` authentication, use the `--kerberos-principal`, `--kerberos-keytab`, and `--kerberos-krb5-conf` parameters\. For more information, see [create\-location\-hdfs](https://docs.aws.amazon.com/cli/latest/reference/datasync/create-location-hdfs.html)\.
  + `agent-arns` – The ARNs of the DataSync agents to use for the HDFS location\.

  The preceding the command returns the location ARN, similar to the following:

  ```
  {
      "arn:aws:datasync:us-east-1:123456789012:location/loc-01234567890example"
  }
  ```

## Creating an object storage location<a name="create-location-object-cli"></a>

An object storage location is the endpoint for an object storage server that's compatible with the Amazon S3 API\. An object storage location defines an object storage server that can be read from or written to\.

For more information about object storage locations, including compatibility requirements, see [Creating an object storage location](create-object-location.md)\. 

**To create an object storage location by using the AWS CLI**
+ Use the following command to create a self\-managed object storage location\.

  ```
  aws datasync create-location-object-storage \
      --server-hostname object-storage-server.example.com \
      --bucket-name DOC-EXAMPLE-BUCKET \
      --agent-arns arn:aws:datasync:us-east-1:123456789012:agent/agent-01234567890deadfb
  ```

  The following parameters are required in the `create-location-object-storage` command\.
  + `server-hostname`: The Domain Name System \(DNS\) name or IP address of the self\-managed object storage server\.
  + `bucket-name`: The name that identifies the bucket on the self\-managed object storage server at the location\.
  + `agent-arns`: The ARNs of the agents to use for the self\-managed object storage location\.

  If your object storage requires a user name and password to authenticate, use the `--access-key` and `--secret-key` parameters to provide the user name and password, respectively\. 

The preceding command returns a location ARN similar to the following\.

```
{
    "arn:aws:datasync:us-east-1:123456789012:location/loc-01234567890deadfb"
}
```

## Creating an Amazon EFS location<a name="create-location-efs-cli"></a>

A *location* is the endpoint for an Amazon EFS file system that can be read from or written to\. You can also create this kind of location by using the console\. For more information, see [Creating an Amazon EFS location](create-efs-location.md)\. 

**To create an Amazon EFS location by using the AWS CLI**

1. If you don't have an Amazon EFS file system, create one\. For information about how to create an EFS file system, see [Getting started with Amazon Elastic File System](https://docs.aws.amazon.com/efs/latest/ug/getting-started.html) in the *Amazon Elastic File System User Guide*\.

1. Identify a subnet that has at least one mount target for that file system\. You can see all the mount targets and the subnets associated with an EFS file system by using the `describe-mount-targets` command\.

   ```
   aws efs describe-mount-targets \
       --region aws-region  \
       --file-system-id file-system-id
   ```
**Note**  
The AWS Region that you specify is the one where your target S3 bucket or EFS file system is located\.

   This command returns information about the target similar to the information shown following\.

   ```
   {
       "MountTargets": [
           {
               "OwnerId": "111222333444",
               "MountTargetId": "fsmt-22334a10",
               "FileSystemId": "fs-123456ab",
               "SubnetId": "subnet-f12a0e34",
               "LifeCycleState": "available",
               "IpAddress": "11.222.0.123",
               "NetworkInterfaceId": "eni-1234a044"
           }
       ]
   }
   ```

1. Specify an Amazon EC2 security group that can access the mount target\. You can run the following command to find out the security group of the mount target\.

   ```
   aws efs describe-mount-target-security-groups \
       --region aws-region \
       --mount-target-id mount-target-id
   ```

   The security group that you provide must be able to communicate with the security group on the mount target in the subnet specified\. 

   The relationship between security group M on the mount target and security group S, which you provide for DataSync to use at this stage, is as follows:
   + Security group M, which you associate with the mount target, must allow inbound access for the TCP protocol on the NFS port \(2049\) from security group S\.

     You can enable an inbound connection either by its IP address \(CIDR range\) or its security group\.
   + Security group S, which you provide to DataSync to access Amazon EFS, should have a rule that enables outbound connections to the NFS port\. It enables outbound connections on one of the file system's mount targets\.

     You can enable outbound connections either by IP address \(CIDR range\) or security group\.

     For information about security groups and mount targets, see [Security groups for Amazon EC2 instances and mount targets](https://docs.aws.amazon.com/efs/latest/ug/security-considerations.html#network-access) in the *Amazon Elastic File System User Guide\.*

1. Create the location\. To create the EFS location, you need the ARNs for your Amazon EC2 subnet, Amazon EC2 security group, and a file system\. Because the DataSync API accepts fully qualified ARNs, you can construct these ARNs\. For information about how to construct ARNs for different services, see [Amazon Resource Names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) in the *AWS General Reference*\. 

   Use the following command to create an EFS location\.

   ```
   aws datasync create-location-efs \
       --subdirectory /path/to/your/subdirectory \
       --efs-filesystem-arn 'arn:aws:elasticfilesystem:region:account-id:file-system/filesystem-id' \
       --ec2-config SecurityGroupArns='arn:aws:ec2:region:account-id:security-group/security-group-id',SubnetArn='arn:aws:ec2:region:account-id:subnet/subnet-id'
   ```

**Note**  
The AWS Region that you specify is the one where your target S3 bucket or EFS file system is located\.

The command returns a location ARN similar to the one shown following\.

```
{ 
    "LocationArn": "arn:aws:datasync:us-west-2:111222333444:location/loc-07db7abfc326c50fb" 
}
```

## Creating an Amazon FSx for Windows File Server location<a name="create-location-fsx-cli"></a>

A *location* is an endpoint for an FSx for Windows File Server that you can read from or write to\. 

You can also create an FSx for Windows File Server location by using the console\. For more information, see [Creating an Amazon FSx for Windows File Server location](create-fsx-location.md)\. 

**To create an FSx for Windows File Server location by using the AWS CLI**
+ Use the following command to create an Amazon FSx location\.

  ```
  aws datasync create-location-fsx-windows \
      --fsx-filesystem-arn arn:aws:fsx:region:account-id:file-system/filesystem-id \
      --security-group-arns arn:aws:ec2:region:account-id:security-group/group-id \
      --user smb-user --password password
  ```

  In the `create-location-fsx-windows` command, specify the following:
  + `fsx-filesystem-arn` – The fully qualified Amazon Resource Name \(ARN\) of the file system that you want to read from or write to\. 

    The DataSync API accepts fully qualified ARNs, and you can construct these ARNs\. For information about how to construct ARNs for different services, see [Amazon Resource Names \(ARNs\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) in the *AWS General Reference*\. 
  + `security-group-arns` – The ARN of an Amazon EC2 security group that can be applied to the [elastic network interfaces](datasync-network.md#required-network-interfaces) of the file system's preferred subnet\. For more information, see [Creating an Amazon VPC with an instance tenancy of dedicated](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html#creatingdedicatedvpc) in the *Amazon EC2 User Guide\.*
  + The AWS Region – The Region that you specify is the one where your target Amazon FSx file system is located\.

The preceding command returns a location ARN similar to the one shown following\.

```
{ 
    "LocationArn": "arn:aws:datasync:us-west-2:111222333444:location/loc-07db7abfc326c50fb" 
}
```

## Creating an Amazon FSx for Lustre location<a name="create-location-lustre-cli"></a>

A *location* is an endpoint for an FSx for Lustre file system that you can read or write to\. 

You can also create an FSx for Lustre location by using the console\. For more information, see [Creating an Amazon FSx for Lustre location](create-lustre-location.md)\.

**To create an FSx for Lustre location by using the AWS CLI**
+ Use the following command to create an FSx for Lustre location\.

  ```
  aws datasync create-location-fsx-lustre \
      --fsx-filesystem-arn arn:aws:fsx:region:account-id:file-system:filesystem-id \
      --security-group-arns arn:aws:ec2:region:account-id:security-group/group-id
  ```

  The following parameters are required in the `create-location-fsx-lustre` command\.
  + `fsx-filesystem-arn` – The fully qualified Amazon Resource Name \(ARN\) of the file system that you want to read from or write to\.
  + `security-group-arns` – The ARN of an Amazon EC2 security group to apply to the network interfaces of the file system's preferred subnet\. For more information, see [Dedicated Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html#creatingdedicatedvpc) in the *Amazon Elastic Compute Cloud User Guide for Linux Instances*\.

The preceding command returns a location ARN similar to the following\.

```
{
    "LocationArn": "arn:aws:datasync:us-west-2:111222333444:location/loc-07sb7abfc326c50fb"
}
```

## Creating an Amazon FSx for OpenZFS location<a name="create-openzfs-location-cli"></a>

A *location* is an endpoint for an FSx for OpenZFS file system that DataSync can access for a transfer\. You also can create an [FSx for OpenZFS location in the console](create-openzfs-location.md)\.

**To create an FSx for OpenZFS location by using the AWS CLI**

1. Copy the following command:

   ```
   $ aws datasync create-location-fsx-openzfs \
      --fsx-filesystem-arn arn:aws:fsx:region:account-id:file-system/filesystem-id \
      --security-group-arns arn:aws:ec2:region:account-id:security-group/group-id \
      --protocol NFS={}
   ```

1. Specify the following required options in the command:
   + For `fsx-filesystem-arn`, specify the location file system's fully qualified Amazon Resource Name \(ARN\)\. This includes the AWS Region where your file system resides, your AWS account, and the file system ID\.
   + For `security-group-arns`, specify the ARN of the Amazon EC2 security group that provides access to the network interfaces of your FSx for OpenZFS file system's preferred subnet\. This includes the AWS Region where your Amazon EC2 instance resides, your AWS account, and the security group ID\.

     For more information about security groups, see [File System Access Control with Amazon VPC](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/limit-access-security-groups.html) in the *Amazon FSx for OpenZFS User Guide*\.
   + For `protocol`, specify the protocol that DataSync uses to access your file system\. \(DataSync currently supports only NFS\.\)

1. Run the command\. You get a response showing the location that you just created\.

   ```
   { 
       "LocationArn": "arn:aws:datasync:us-west-2:123456789012:location/loc-abcdef01234567890" 
   }
   ```

## Creating an Amazon FSx for NetApp ONTAP location<a name="create-ontap-location-cli"></a>

A *location* is an endpoint for an FSx for ONTAP file system that DataSync can access for a transfer\. You also can create an [FSx for ONTAP location in the console](create-ontap-location.md)\.

**To create an FSx for ONTAP location by using the AWS CLI**

1. Copy the following command:

   ```
   $ aws datasync create-location-fsx-ontap \
      --storage-virtual-machine-arn arn:aws:fsx:region:account-id:storage-virtual-machine/fs-file-system-id \
      --security-group-arns arn:aws:ec2:region:account-id:security-group/group-id \
      --protocol data-transfer-protocol={}
   ```

1. Specify the following required options in the command:
   + For `storage-virtual-machine-arn`, specify the fully qualified Amazon Resource Name \(ARN\) of a storage virtual machine \(SVM\) in your file system where you want to copy data to or from\.

     This ARN includes the AWS Region where your file system resides, your AWS account, and the file system and SVM IDs\.
   + For `security-group-arns`, specify the ARNs of the Amazon EC2 security groups that provide access to the network interfaces of your file system's preferred subnet\.

     This includes the AWS Region where your Amazon EC2 instance resides, your AWS account, and your security group IDs\. You can specify up to five security group ARNs\.

     For more information about security groups, see [File System Access Control with Amazon VPC](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/limit-access-security-groups.html) in the *Amazon FSx for NetApp ONTAP User Guide*\.
   + For `protocol`, configure the protocol that DataSync uses to access your file system's SVM\.
     + For NFS, you can use the default configuration:

       `--protocol NFS={}`
     + For SMB, you must specify a user name and password that can access the SVM:

       `--protocol SMB={User=smb-user,Password=smb-password}`

1. Run the command\.

   You get a response that shows the location that you just created\.

   ```
   { 
       "LocationArn": "arn:aws:datasync:us-west-2:123456789012:location/loc-abcdef01234567890" 
   }
   ```

## Creating an Amazon S3 location<a name="create-location-s3-cli"></a>

An Amazon S3 location requires an S3 bucket that can be read from or written to\. To create an S3 bucket, see [Creating a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) in the *Amazon S3 User Guide*\. 

For DataSync to access an S3 bucket, DataSync needs an AWS Identity and Access Management \(IAM\) role that has the required permissions\. With the following procedure, you create the IAM role, the required IAM policies, and the S3 location by using the AWS CLI\. 

For DataSync to assume the IAM role, AWS Security Token Service \(AWS STS\) must be activated in your account and Region\. For more information about temporary security credentials, see [Temporary security credentials in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html) in the *IAM User Guide*\. 

You can also create an S3 location by using the console\. For more information, see [Creating an Amazon S3 location](create-s3-location.md)\. 

**To create an S3 location by using the CLI**

1. Create an IAM trust policy that allows DataSync to assume the IAM role required to access your S3 bucket\.

   The following is an example of a trust policy\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "datasync.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

1. Create a temporary file for the IAM policy, as shown in the following example\.

   ```
   $ ROLE_FILE=$(mktemp -t sync.iam.role.filename.json)
   $ IAM_ROLE_NAME='YourBucketAccessRole'
   
   $ cat<<EOF> ${ROLE_FILE}
   {
       "Version": "2012-10-17",
       "Statement": [{
           "Effect": "Allow",
           "Principal": {
               "Service": "datasync.amazonaws.com"
           },
           "Action": "sts:AssumeRole"
       }]
   }
   ```

1. Create an IAM role and attach the IAM policy to it\.

   The following command creates an IAM role and attaches the policy to it\. 

   ```
   $ aws iam create-role --role-name ${IAM_ROLE_NAME} --assume-role-policy-document file://${ROLE_FILE}
   {
       "Role": {
           "Path": "/",
           "RoleName": "YourBucketAccessRole",
           "RoleId": "role-id",
           "Arn": "arn:aws:iam::account-id:role/YourBucketAccessRole",
           "CreateDate": "2018-07-27T02:49:23.117Z",
           "AssumeRolePolicyDocument": {
               "Version": "2012-10-17",
               "Statement": [{
                   "Effect": "Allow",
                   "Principal": {
                       "Service": "datasync.amazonaws.com"
                   },
                   "Action": "sts:AssumeRole"
               }]
           }
       }
   }
   ```

1. Allow the IAM role that you created to write to your S3 bucket\.

   Attach to the IAM role an IAM policy that has sufficient permissions to access your S3 bucket\. The following example shows the minimum permissions needed for DataSync to read and write to an S3 bucket in an AWS Region\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Action": [
                   "s3:GetBucketLocation",
                   "s3:ListBucket",
                   "s3:ListBucketMultipartUploads"
               ],
               "Effect": "Allow",
               "Resource": "YourS3BucketArn"
           },
           {
               "Action": [
                   "s3:AbortMultipartUpload",
                   "s3:DeleteObject",
                   "s3:GetObject",
                   "s3:ListMultipartUploadParts",
                   "s3:PutObjectTagging",
                   "s3:GetObjectTagging",
                   "s3:PutObject"
               ],
               "Effect": "Allow",
               "Resource": "YourS3BucketArn/*"
           }
       ]
   }
   ```

   To attach the policy to your IAM role, run the following command\.

   ```
   $ aws iam attach-role-policy \
       --role-name role-name  \
       --policy-arn 'arn:aws:iam::aws:policy/YourPolicyName'
   ```

   For Amazon S3 buckets on AWS Outposts, use the following policy\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [{
               "Action": [
                   "s3-outposts:ListBucket",
                   "s3-outposts:ListBucketMultipartUploads"
               ],
               "Effect": "Allow",
               "Resource": [
                   "s3OutpostsBucketArn",
                   "s3OutpostsAccessPointArn"
               ],
               "Condition": {
                   "StringLike": {
                       "s3-outposts:DataAccessPointArn": "s3OutpostsAccessPointArn"
                   }
               }
           },
           {
               "Action": [
                   "s3-outposts:AbortMultipartUpload",
                   "s3-outposts:DeleteObject",
                   "s3-outposts:GetObject",
                   "s3-outposts:ListMultipartUploadParts",
                   "s3-outposts:PutObjectTagging",
                   "s3-outposts:GetObjectTagging",
                   "s3-outposts:PutObject"
               ],
               "Effect": "Allow",
               "Resource": [
                   "s3OutpostsBucketArn/*",
                   "s3OutpostsAccessPointArn"
               ],
               "Condition": {
                   "StringLike": {
                       "s3-outposts:DataAccessPointArn": "s3OutpostsAccessPointArn"
                   }
               }
           },
           {
               "Effect": "Allow",
               "Action": [
                   "s3-outposts:GetAccessPoint"
               ],
               "Resource": "s3OutpostsAccessPointArn"
           }
       ]
   }
   ```

1. Create the S3 location\.

   Use the following command to create your Amazon S3 location\.

   ```
   $ aws datasync create-location-s3 \
       --s3-bucket-arn 'arn:aws:s3:::DOC-EXAMPLE-BUCKET' \
       --s3-storage-class 'your-S3-storage-class' \
       --s3-config 'BucketAccessRoleArn=arn:aws:iam::account-id:role/role-allowing-DS-operations' \
       --subdirectory /your-folder
   ```

   The command returns a location ARN similar to the one shown following\.

   ```
   {
       "LocationArn": "arn:aws:datasync:us-east-1:111222333444:location/loc-0b3017fc4ba4a2d8d"
   }
   ```

   The location type information is encoded in the `LocationUri`\. In this example, the `s3://` prefix in `LocationUri` shows the location's type\.

   If your Amazon S3 bucket is located on an AWS Outpost, you must deploy an Amazon EC2 agent on your Outpost\. The agent must be in a virtual private cloud \(VPC\) that's allowed to access the access point specified in the command\. The agent also must be activated in the parent Region for the Outpost, and be able to route to the Amazon S3 on AWS Outposts endpoints for the bucket\. For more information about launching a DataSync agent on AWS Outposts, see [Deploy your agent on AWS Outposts](deploy-agents.md#outposts-agent)\.

   Use the following command to create an Amazon S3 location on your Outpost\.

   ```
   aws datasync create-location-s3 \
       --s3-bucket-arn access-point-arn \
       --s3-config BucketAccessRoleArn=arn:aws:iam::account-id:role/role-allowing-DS-operations \
       --agent-arns arn-of-datasync-agent-in-vpc-that-can-access-your-s3-access-point
   ```

**Note**  
Changes to object data or metadata are equivalent to deleting an object and creating a new one to replace it\. This results in additional charges in the following scenarios:  
**When using object versioning** – Changes to object data or metadata create a new version of the object\.
**When using storage classes that can incur additional charges for overwriting, deleting, or retrieving, objects** – Changes to object data or metadata result in such charges\. For more information, see [Storage class considerations with Amazon S3 locations](create-s3-location.md#using-storage-classes)\. 
When you use object versioning, a single DataSync task execution might create more than one version of an Amazon S3 object\.
In addition to the IAM policies that grant DataSync permissions, we recommend creating a multipart upload bucket policy for your S3 buckets\. Doing this can help you control your storage costs\. For more information, see the blog post [ S3 lifecycle management update \- support for multipart uploads and delete markers](http://aws.amazon.com/blogs/aws/s3-lifecycle-management-update-support-for-multipart-uploads-and-delete-markers/)\.