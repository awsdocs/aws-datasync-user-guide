# Creating a location for HDFS<a name="create-hdfs-location"></a>

When you create a location in a task, you configure it as the source or destination location\.

To connect to your Hadoop Distributed File System \(HDFS\) cluster, AWS DataSync uses an agent\. The agent is a virtual machine that you deploy near your HDFS cluster\. To learn more about DataSync agents, see [Working with agents](working-with-agents.md)\. The DataSync agent acts as an HDFS client and communicates with the NameNodes and DataNodes in your clusters\. 

When you start a task, DataSync queries the NameNode for locations of files and folders on the cluster\. If the HDFS location is configured as a source, then DataSync reads files and folder data from the DataNodes in the cluster and copies the data to the destination\. If the HDFS location is configured as a destination, then DataSync writes files and folders from the destination to the DataNodes in the cluster\. Before running your DataSync task, verify agent connectivity to the HDFS cluster\. For more information, see [Testing connectivity to self\-managed storage](local-console-vm.md#self-managed-storage-connectivity)\.

**Authentication**  
When connecting to an HDFS cluster, DataSync supports simple authentication or Kerberos authentication\. To use simple authentication, provide the user name of a user with rights to read and write to the HDFS cluster\. To use Kerberos authentication, provide a Kerberos configuration file, a Kerberos key table \(keytab\) file, and a Kerberos principal name\. The credentials of the Kerberos principal must be in the provided keytab file\.

**Encryption**  
When using Kerberos authentication, DataSync supports encryption of data as it's transmitted between the DataSync agent and your HDFS cluster\. Encrypt your data by using the Quality of Protection \(QOP\) configuration settings on your HDFS cluster and by specifying the QOP settings when creating your HDFS location\. The QOP configuration includes settings for data transfer protection and Remote Procedure Call \(RPC\) protection\. 

**DataSync supports the following Kerberos encryption types:**
+ des\-cbc\-crc
+ des\-cbc\-md4
+ des\-cbc\-md5
+ des3\-cbc\-sha1
+ arcfour\-hmac
+ arcfour\-hmac\-exp
+ aes128\-cts\-hmac\-sha1\-96
+ aes256\-cts\-hmac\-sha1\-96
+ aes128\-cts\-hmac\-sha256\-128
+ aes256\-cts\-hmac\-sha384\-192
+ camellia128\-cts\-cmac
+ camellia256\-cts\-cmac

You can also configure HDFS clusters for encryption at rest using Transparent Data Encryption \(TDE\)\. When using simple authentication, DataSync reads and writes to TDE\-enabled clusters\. If you're using DataSync to copy data to a TDE\-enabled cluster, first configure the encryption zones on the HDFS cluster\. DataSync doesn't create encryption zones\. 

**Note**  
Before creating your HDFS location, verify network connectivity between your agent and your Hadoop cluster\. Test access to the TCP ports listed in the [ Network requirements to connect to your self\-managed storage ](datasync-network.md#on-premises-network-requirements) table\. To test access between your local agent and your Hadoop cluster, follow the procedure in [Testing connectivity to self\-managed storage](local-console-vm.md#self-managed-storage-connectivity)\.

**To create an HDFS location**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. On the **Locations** page, choose **Create location**\.

1. For the **Location type**, choose **Hadoop Distributed File System \(HDFS\)**\. You can configure this location as a source or destination later\. 

1. For **Agents**, choose one or more agents that you want to use from the list of available agents\. The agent connects to your HDFS cluster to securely transfer data between the HDFS cluster and DataSync\. 

1. For **NameNode**, provide the domain name or IP address of the HDFS cluster's primary NameNode\.

1. For **Folder**, enter a folder on your HDFS cluster that DataSync will use for the data transfer\. When the location is used as a source for a task, DataSync copies files in the provided folder\. When your location is used as a destination for a task, DataSync writes all files to the provided folder\.

1. To set the **Block size** or **Replication factor**, choose **Additional settings**\. The default block size is 128 MiB, and any provided block sizes must be a multiple of 512 bytes\. The default replication factor is three DataNodes when transferring data to the HDFS cluster\. 

1. In the **Security** section, choose the **Authentication type** used on your HDFS cluster\. 
   + **Simple**: Provide the user name of the **User** with read and write permissions on the HDFS cluster\. Optionally, provide the URI of the Key Management Server \(KMS\) of the HDFS cluster\. 
   + **Kerberos**: Provide the Kerberos **Principal** with access to your HDFS cluster\. Next, provide the **KeyTab file** that contains the provided Kerberos principal\. Then, provide the **Kerberos configuration file**\. Finally, specify the type of encryption in transit protection in the **RPC protection** and **Data transfer protection** dropdown lists\.

1. \(Optional\) **Tags** are key\-value pairs that help you manage, filter, and search for your location\. Adding a tag is optional\. We recommend using tags for naming your resources\. 

1. When you're done, choose **Create location**\.

## Unsupported HDFS features<a name="hdfs-unsupported-deatures"></a>

The following capabilities of HDFS aren't currently supported by DataSync:
+ Transparent Data Encryption \(TDE\) when using Kerberos authentication
+ Configuring multiple NameNodes
+ Hadoop HDFS over HTTP \(HttpFS\)
+ POSIX access control lists \(ACLs\)
+ HDFS extended attributes \(xattrs\)