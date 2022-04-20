# Configuring your DataSync agent for multiple NICs<a name="configure-agent-multinic"></a>

If you configure your agent to use multiple network adapters \(NICs\), the agent can be accessed by more than one IP address\. You might want to do this in the following situations:
+ ****Maximizing throughput**** – You might want to maximize throughput to an agent when network adapters are a bottleneck\.
+ ****Network isolation**** – Your Network File System \(NFS\), Server Message Block \(SMB\), Hadoop Distributed File System \(HDFS\), or object storage server might reside on a virtual LAN \(VLAN\) that lacks internet connectivity for security reasons\.

In a typical multiple\-adapter use case, one adapter is configured as the route by which the agent communicates with AWS \(as the default agent\)\. Except for this one adapter, NFS, SMB, HDFS, or self\-managed object storage locations must be in the same subnet as the adapter that connects to them\. Otherwise, communication with the intended NFS, SMB, HDFS, or object storage locations might not be possible\. In some cases, you might configure an NFS, SMB, HDFS, or object storage location on the same adapter that's used for communication with AWS\. In these cases, NFS, SMB, HDFS, or object storage traffic for that server and AWS traffic flows through the same adapter\.

In some cases, you might configure one adapter to connect to the AWS DataSync console and then add a second adapter\. In such a case, DataSync automatically configures the route table to use the second adapter as the preferred route\. 