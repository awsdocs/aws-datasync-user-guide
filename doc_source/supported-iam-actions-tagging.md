# Granting permission to tag AWS DataSync resources during creation<a name="supported-iam-actions-tagging"></a>

Some resource\-creating AWS DataSync API actions enable you to specify tags when you create the resource\. You can use resource tags to implement attribute\-based access control \(ABAC\)\. For more information, see  [ What is ABAC for AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html) in the *IAM User Guide*\.

To enable users to tag resources on creation, they must have permissions to use the action that creates the resource \(such as `datasync:CreateAgent` or `datasync:CreateTask`\)\. If tags are specified in the resource\-creating action, users must also have explicit permissions to use the `datasync:TagResource` action\.

The `datasync:TagResource` action is only evaluated if tags are applied during the resource\-creating action\. Therefore, a user that has permissions to create a resource \(assuming there are no tagging conditions\) doesn't require permissions to use the `datasync:TagResource` action if no tags are specified in the request\.

However, if the user attempts to create a resource with tags, the request fails if the user doesn't have permissions to use the `datasync:TagResource` action\.

## Example IAM policy statements<a name="supported-iam-actions-tagging-examples"></a>

Use the following example IAM policy statements to grant `TagResource` permissions to users creating DataSync resources\.

The following statement allows users to tag a DataSync agent when they create the agent\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
       "Effect": "Allow",
       "Action": "datasync:TagResource",
       "Resource": "arn:aws:datasync:region:account-id:agent/*"
    }
  ]
}
```

The following statement allows users to tag a DataSync location when they create the location\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "datasync:TagResource",
            "Resource": "arn:aws:datasync:region:account-id:location/*"
        }
    ]
}
```

The following statement allows users to tag a DataSync task when they create the task\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "datasync:TagResource",
            "Resource": "arn:aws:datasync:region:account-id:task/*"
        }
    ]
}
```