# FsxProtocol<a name="API_FsxProtocol"></a>

Specifies the data transfer protocol that AWS DataSync uses to access your Amazon FSx file system\.

## Contents<a name="API_FsxProtocol_Contents"></a>

 ** NFS **   <a name="DataSync-Type-FsxProtocol-NFS"></a>
Specifies the Network File System \(NFS\) protocol configuration that DataSync uses to access your FSx for OpenZFS file system or FSx for ONTAP file system's storage virtual machine \(SVM\)\.  
Type: [FsxProtocolNfs](API_FsxProtocolNfs.md) object  
Required: No

 ** SMB **   <a name="DataSync-Type-FsxProtocol-SMB"></a>
Specifies the Server Message Block \(SMB\) protocol configuration that DataSync uses to access your FSx for ONTAP file system's SVM\.  
Type: [FsxProtocolSmb](API_FsxProtocolSmb.md) object  
Required: No

## See Also<a name="API_FsxProtocol_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/FsxProtocol) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/FsxProtocol) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/FsxProtocol) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/FsxProtocol) 