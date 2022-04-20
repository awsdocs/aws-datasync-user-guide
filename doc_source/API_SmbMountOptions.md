# SmbMountOptions<a name="API_SmbMountOptions"></a>

Represents the mount options that are available for DataSync to access an SMB location\.

## Contents<a name="API_SmbMountOptions_Contents"></a>

 ** Version **   <a name="DataSync-Type-SmbMountOptions-Version"></a>
The specific SMB version that you want DataSync to use to mount your SMB share\. If you don't specify a version, DataSync defaults to `AUTOMATIC`\. That is, DataSync automatically selects a version based on negotiation with the SMB server\.  
Type: String  
Valid Values:` AUTOMATIC | SMB2 | SMB3`   
Required: No

## See Also<a name="API_SmbMountOptions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/SmbMountOptions) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/SmbMountOptions) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/SmbMountOptions) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/SmbMountOptions) 