# DataSync API permissions: Actions and resources<a name="datasync-api-permissions-ref"></a>

When creating AWS Identity and Access Management \(IAM\) policies, this page can help you understand the relationship between AWS DataSync API operations, the corresponding actions that you can grant permissions to perform, and the AWS resources for which you can grant the permissions\.

In general, here's how you add DataSync permissions to your policy:
+ Specify an action in the `Action` element\. The value includes a `datasync:` prefix and the API operation name\. For example, `datasync:CreateTask`\.
+ Specify an AWS resource related to the action in the `Resource` element\. 

You can also use AWS condition keys in your DataSync policies\. For a complete list of AWS keys, see [Available keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.

For a list of DataSync resources and their Amazon Resource Name \(ARN\) formats, see [DataSync resources and operations](managing-access-overview.md#access-control-specify-datasync-actions)\.

Related topics

 
+ [Permissions](managing-access-overview.md#access-control)
+ [Customer managed policy examples](using-identity-based-policies.md#customer-managed-policies)