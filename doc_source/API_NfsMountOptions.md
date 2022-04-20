# NfsMountOptions<a name="API_NfsMountOptions"></a>

Represents the mount options that are available for DataSync to access an NFS location\.

## Contents<a name="API_NfsMountOptions_Contents"></a>

 ** Version **   <a name="DataSync-Type-NfsMountOptions-Version"></a>
The specific NFS version that you want DataSync to use to mount your NFS share\. If the server refuses to use the version specified, the sync will fail\. If you don't specify a version, DataSync defaults to `AUTOMATIC`\. That is, DataSync automatically selects a version based on negotiation with the NFS server\.  
You can specify the following NFS versions:  
+  ** [NFSv3](https://tools.ietf.org/html/rfc1813) ** \- stateless protocol version that allows for asynchronous writes on the server\.
+  ** [NFSv4\.0](https://tools.ietf.org/html/rfc3530) ** \- stateful, firewall\-friendly protocol version that supports delegations and pseudo file systems\.
+  ** [NFSv4\.1](https://tools.ietf.org/html/rfc5661) ** \- stateful protocol version that supports sessions, directory delegations, and parallel data processing\. Version 4\.1 also includes all features available in version 4\.0\.
Type: String  
Valid Values:` AUTOMATIC | NFS3 | NFS4_0 | NFS4_1`   
Required: No

## See Also<a name="API_NfsMountOptions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/NfsMountOptions) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/NfsMountOptions) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/NfsMountOptions) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/NfsMountOptions) 