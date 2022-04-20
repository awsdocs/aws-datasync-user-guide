# Identity and access management in AWS DataSync<a name="iam"></a>

AWS uses security credentials to identify you and to grant you access to your AWS resources\. You can use features of AWS Identity and Access Management \(IAM\) to allow other users, services, and applications to use your AWS resources fully or in a limited way, without sharing your security credentials\.

By default, IAM identities \(users, groups, and roles\) don't have permission to create, view, or modify AWS resources\. To allow users, groups, and roles to access AWS DataSync resources and interact with the DataSync console and API, we recommend that you use an IAM policy that grants them permission to use the specific resources and API actions that they will need\. You then attach the policy to the IAM identity that requires access\. For an overview of the basic elements for a policy, see [Overview of managing access permissions for DataSync](managing-access-overview.md)\.

**Topics**
+ [Overview of managing access permissions for DataSync](managing-access-overview.md)
+ [Using identity\-based policies \(IAM policies\) for DataSync](using-identity-based-policies.md)
+ [Cross\-service confused deputy prevention](cross-service-confused-deputy-prevention.md)
+ [DataSync API permissions: Actions and resources](datasync-api-permissions-ref.md)

The following sections provide details on how you can use [AWS Identity and Access Management \(IAM\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) and DataSync to help secure your resources by controlling who can access them: 
+ [Authentication](managing-access-overview.md#authentication)
+ [Permissions](managing-access-overview.md#access-control) 