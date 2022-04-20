# HdfsNameNode<a name="API_HdfsNameNode"></a>

The NameNode of the Hadoop Distributed File System \(HDFS\)\. The NameNode manages the file system's namespace\. The NameNode performs operations such as opening, closing, and renaming files and directories\. The NameNode contains the information to map blocks of data to the DataNodes\.

## Contents<a name="API_HdfsNameNode_Contents"></a>

 ** Hostname **   <a name="DataSync-Type-HdfsNameNode-Hostname"></a>
The hostname of the NameNode in the HDFS cluster\. This value is the IP address or Domain Name Service \(DNS\) name of the NameNode\. An agent that's installed on\-premises uses this hostname to communicate with the NameNode in the network\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^(([a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9\-]*[A-Za-z0-9])$`   
Required: Yes

 ** Port **   <a name="DataSync-Type-HdfsNameNode-Port"></a>
The port that the NameNode uses to listen to client requests\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65536\.  
Required: Yes

## See Also<a name="API_HdfsNameNode_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/HdfsNameNode) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/HdfsNameNode) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/HdfsNameNode) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/HdfsNameNode) 