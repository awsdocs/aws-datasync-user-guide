# FsxProtocolSmb<a name="API_FsxProtocolSmb"></a>

Specifies the Server Message Block \(SMB\) protocol configuration that AWS DataSync uses to access your Amazon FSx for NetApp ONTAP file system\. For more information, see [Accessing FSx for ONTAP file systems](https://docs.aws.amazon.com/datasync/latest/userguide/create-ontap-location.html#create-ontap-location-access)\.

## Contents<a name="API_FsxProtocolSmb_Contents"></a>

 ** Domain **   <a name="DataSync-Type-FsxProtocolSmb-Domain"></a>
Specifies the fully qualified domain name \(FQDN\) of the Microsoft Active Directory that your storage virtual machine \(SVM\) belongs to\.  
Type: String  
Length Constraints: Maximum length of 253\.  
Pattern: `^[A-Za-z0-9]((\.|-+)?[A-Za-z0-9]){0,252}$`   
Required: No

 ** MountOptions **   <a name="DataSync-Type-FsxProtocolSmb-MountOptions"></a>
Specifies how DataSync can access a location using the SMB protocol\.  
Type: [SmbMountOptions](API_SmbMountOptions.md) object  
Required: No

 ** Password **   <a name="DataSync-Type-FsxProtocolSmb-Password"></a>
Specifies the password of a user who has permission to access your SVM\.  
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^.{0,104}$`   
Required: Yes

 ** User **   <a name="DataSync-Type-FsxProtocolSmb-User"></a>
Specifies a user name that can mount the location and access the files, folders, and metadata that you need in the SVM\.  
If you provide a user in your Active Directory, note the following:  
+ If you're using AWS Directory Service for Microsoft Active Directory, the user must be a member of the AWS Delegated FSx Administrators group\.
+ If you're using a self\-managed Active Directory, the user must be a member of either the Domain Admins group or a custom group that you specified for file system administration when you created your file system\.
Make sure that the user has the permissions it needs to copy the data you want:  
+  `SE_TCB_NAME`: Required to set object ownership and file metadata\. With this privilege, you also can copy NTFS discretionary access lists \(DACLs\)\.
+  `SE_SECURITY_NAME`: May be needed to copy NTFS system access control lists \(SACLs\)\. This operation specifically requires the Windows privilege, which is granted to members of the Domain Admins group\. If you configure your task to copy SACLs, make sure that the user has the required privileges\. For information about copying SACLs, see [Ownership and permissions\-related options](https://docs.aws.amazon.com/datasync/latest/userguide/create-task.html#configure-ownership-and-permissions)\.
Type: String  
Length Constraints: Maximum length of 104\.  
Pattern: `^[^\x5B\x5D\\/:;|=,+*?]{1,104}$`   
Required: Yes

## See Also<a name="API_FsxProtocolSmb_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/datasync-2018-11-09/FsxProtocolSmb) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/datasync-2018-11-09/FsxProtocolSmb) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/datasync-2018-11-09/FsxProtocolSmb) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/datasync-2018-11-09/FsxProtocolSmb) 