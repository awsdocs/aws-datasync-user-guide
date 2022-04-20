# Overview of managing access permissions for DataSync<a name="managing-access-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\), and some services \(such as AWS Lambda\) also support attaching permissions policies to resources\. 

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources that they get permissions for, and the specific actions that you want to allow on those resources\.

**Topics**
+ [DataSync resources and operations](#access-control-specify-datasync-actions)
+ [Understanding resource ownership](#access-control-owner)
+ [Managing access to resources](#access-control-managing-permissions)
+ [Specifying policy elements: Actions, effects, resources, and principals](#policy-elements)
+ [Specifying conditions in a policy](#specifying-conditions)
+ [Controlling access](#aws-access)

## DataSync resources and operations<a name="access-control-specify-datasync-actions"></a>

In DataSync, the primary resources are task, location, agent, and task execution\.

These resources have unique Amazon Resource Names \(ARNs\) associated with them, as shown in the following table\.


| Resource type | ARN format | 
| --- | --- | 
| Task ARN |  `arn:aws:datasync:region:account-id:task/task-id `  | 
| Location ARN |  `arn:aws:datasync:region:account-id:location/location-id`  | 
|  Agent ARN  |  `arn:aws:datasync:region:account-id:agent/agent-id`  | 
| Task execution ARN |  `arn:aws:datasync:region:account-id:task/task-id/execution/exec-id`  | 

To grant permissions for specific API operations, such as creating a task, DataSync defines a set of actions that you can specify in a permissions policy\. An API operation can require permissions for more than one action\. For a list of all the DataSync API actions and the resources that they apply to, see [DataSync API permissions: Actions and resources](datasync-api-permissions-ref.md)\.

## Understanding resource ownership<a name="access-control-owner"></a>

A *resource owner* is the AWS account that created the resource\. That is, the resource owner is the AWS account of the *principal entity* \(the root account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this behavior works:

 
+ If you use the root account credentials of your AWS account to create a task, your AWS account is the owner of the resource \(in DataSync, the resource is the task\)\.
+ If you create an IAM user in your AWS account and grant permissions to the `CreateTask` action to that user, the user can create a task\. However, your AWS account, to which the user belongs, owns the task resource\.
+ If you create an IAM role in your AWS account with permissions to create a task, anyone who can assume the role can create a task\. Your AWS account, to which the role belongs, owns the task resource\. 

## Managing access to resources<a name="access-control-managing-permissions"></a>

A permissions policy describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of DataSync\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide\.* For information about IAM policy syntax and descriptions, see [AWS Identity and Access Management policy reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide\.*

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM policies\) and policies attached to a resource are referred to as *resource\-based* policies\. DataSync supports only identity\-based policies \(IAM policies\)\. 

**Topics**
+ [Identity\-based policies \(IAM policies\)](#identity-based-policies)
+ [Resource\-based policies](#resource-based-policies)

### Identity\-based policies \(IAM policies\)<a name="identity-based-policies"></a>

You can attach policies to IAM identities\. For example, you can do the following:
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create a DataSync resource, such as a task, location, agent, or task execution\.
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. The Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. The Account A administrator attaches a trust policy to the role that identifies Account B as the principal who can assume the role\. 

     To grant an AWS service permissions to assume the role, the Account A administrator can specify an AWS service as the principal in the trust policy\.

  1. The Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. 

  For more information about using IAM to delegate permissions, see [Access management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

The following example policy grants permissions to all `List*` actions on all resources\. This action is a read\-only action\. Thus, the policy doesn't allow the user to change the state of the resources\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAllListActionsOnAllResources",
            "Effect": "Allow",
            "Action": [
                "datasync:List*"
            ],
            "Resource": "*"
        }
    ]
}
```

For more information about using identity\-based policies with DataSync, see [Using identity\-based policies \(IAM policies\) for DataSync](using-identity-based-policies.md)\. For more information about users, groups, roles, and permissions, see [Identities \(users, groups, and roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-based policies<a name="resource-based-policies"></a>

Other services, such as Amazon S3, support resource\-based permissions policies\. For example, you can attach a policy to an Amazon S3 bucket to manage access permissions to that bucket\. However, DataSync doesn't support resource\-based policies\. 

## Specifying policy elements: Actions, effects, resources, and principals<a name="policy-elements"></a>

For each DataSync resource \(see [DataSync API permissions: Actions and resources](datasync-api-permissions-ref.md)\), the service defines a set of API operations \(see [Actions](https://docs.aws.amazon.com/datasync/latest/userguide/API_Operations.html)\)\. To grant permissions for these API operations, DataSync defines a set of actions that you can specify in a policy\. For example, for the DataSync resource, the following actions are defined: `CreateTask`, `DeleteTask`, and `DescribeTask`\. Performing an API operation can require permissions for more than one action\.

The following are the most basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For DataSync resources, you can use the wildcard character `(*)` in IAM policies\. For more information, see [DataSync resources and operations](#access-control-specify-datasync-actions)\.
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, depending on the specified `Effect` element, the `datasync:CreateTask` permission allows or denies the user permissions to perform the DataSync `CreateTask` operation\.
+ **Effect** – You specify the effect when the user requests the specific action—this effect can be either `Allow` or `Deny`\. If you don't explicitly grant access to \(`Allow`\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants that user access\. For more information, see [ Authorization](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html#intro-structure-authorization) in the *IAM User Guide*\. 
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. DataSync doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS Identity and Access Management policy reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the DataSync API actions, see [DataSync API permissions: Actions and resources](datasync-api-permissions-ref.md)\.

## Specifying conditions in a policy<a name="specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions when a policy should take effect when granting permissions\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to DataSync\. However, there are AWS wide condition keys that you can use as appropriate\. For a complete list of AWS wide keys, see [Available keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

## Controlling access<a name="aws-access"></a>

In this section, you can find information about how to control access to AWS resources\.

### Authentication<a name="authentication"></a>

You can access AWS as any of the following types of identities:
+ **AWS account root user** –  When you first create an AWS account, you begin with a single sign\-in identity that has complete access to all AWS services and resources in the account\. This identity is called the AWS account *root user* and is accessed by signing in with the email address and password that you used to create the account\. We strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones\. Instead, adhere to the [best practice of using the root user only to create your first IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#create-iam-users)\. Then securely lock away the root user credentials and use them to perform only a few account and service management tasks\. 
+ **IAM user** – An [IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) is an identity within your AWS account that has specific custom permissions \(for example, permissions to create a task in DataSync\)\. You can use an IAM user name and password to sign in to secure AWS webpages like the [AWS Management Console](https://console.aws.amazon.com/), [AWS Discussion Forums](https://forums.aws.amazon.com/), or the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

  In addition to a user name and password, you can also generate [access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for each user\. You can use these keys when you access AWS services programmatically, either through [one of the several SDKs](https://aws.amazon.com/tools/#sdk) or by using the [AWS Command Line Interface \(CLI\)](https://aws.amazon.com/cli/)\. The SDK and CLI tools use the access keys to cryptographically sign your request\. If you don’t use AWS tools, you must sign the request yourself\. DataSync supports *Signature Version 4*, a protocol for authenticating inbound API requests\. For more information about authenticating requests, see [Signature Version 4 signing process](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html) in the *AWS General Reference*\.
+ **IAM role** –  An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an IAM identity that you can create in your account that has specific permissions\. An IAM role is similar to an IAM user in that it is an AWS identity with permissions policies that determine what the identity can and cannot do in AWS\. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it\. Also, a role does not have standard long\-term credentials such as a password or access keys associated with it\. Instead, when you assume a role, it provides you with temporary security credentials for your role session\. IAM roles with temporary credentials are useful in the following situations:
  + **Federated user access** –  Instead of creating an IAM user, you can use existing identities from AWS Directory Service, your enterprise user directory, or a web identity provider\. These are known as *federated users*\. AWS assigns a role to a federated user when access is requested through an [identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html)\. For more information about federated users, see [Federated users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html#intro-access-roles) in the *IAM User Guide*\. 
  + **AWS service access** –  A service role is an [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) that a service assumes to perform actions on your behalf\. An IAM administrator can create, modify, and delete a service role from within IAM\. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html) in the *IAM User Guide*\. 
  + **Applications running on Amazon EC2** –  You can use an IAM role to manage temporary credentials for applications that are running on an EC2 instance and making AWS CLI or AWS API requests\. This is preferable to storing access keys within the EC2 instance\. To assign an AWS role to an EC2 instance and make it available to all of its applications, you create an instance profile that is attached to the instance\. An instance profile contains the role and enables programs that are running on the EC2 instance to get temporary credentials\. For more information, see [Using an IAM role to grant permissions to applications running on Amazon EC2 instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html) in the *IAM User Guide*\. 

### Permissions<a name="access-control"></a>

You can have valid credentials to authenticate your requests, but unless you have permissions, you cannot create or access DataSync resources\. For example, you must have permissions to create a task in DataSync\.

The following sections provide an overview and describe how to manage permissions for DataSync\.
+ [Overview of managing access permissions for DataSync](#managing-access-overview)
+ [Identity\-based policies \(IAM policies\)](#identity-based-policies)