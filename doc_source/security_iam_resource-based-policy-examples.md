# Amazon Connect Resource\-Based Policy Examples<a name="security_iam_resource-based-policy-examples"></a>

Amazon Connect supports resource\-level permissions for IAM users, so you can specify actions for them for an instance, as shown in the following policies\.

## Deny the "Delete" and "Update" Actions<a name="connect-access-control-resources-example1"></a>

This following sample policy denies the "delete" and "update" actions for users in one Amazon Connect instance\. It uses a wild card at the end of the Amazon Connect user ARN so that "delete user" and "update user" are denied on the full user ARN \(that is, all Amazon Connect users in the provided instance, such as arn:aws:connect:us\-east\-1:123456789012:instance/00fbeee1\-123e\-111e\-93e3\-11111bfbfcc1/agent/00dtcddd1\-123e\-111e\-93e3\-11111bfbfcc1\)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "connect:DeleteUser",
                "connect:UpdateUser*"
            ],
            "Resource": "arn:aws:connect:us-east-1:123456789012:instance/00fbeee1-123e-111e-93e3-11111bfbfcc1/agent/*"
        }
    ]
}
```

## Allow "Create Users" But Deny If You're Assigned to a Specific Security Profile<a name="connect-access-control-resources-example2"></a>

The following sample policy allows "create users" but explicitly denies using arn:aws:connect:us\-west\-2:123456789012:instance/00fbeee1\-123e\-111e\-93e3\-11111bfbfcc1/security\-profile/11dtcggg1\-123e\-111e\-93e3\-11111bfbfcc17 as the parameter for security profile in [CreateUser](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateUser.html#API_CreateUser_RequestBody) request\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",        
            "Action": [
                "connect:CreateUser"
             ],
            "Resource": "*",
        },
        {
            "Effect": "Deny",
            "Action": [
                "connect:CreateUser"
             ],
            "Resource": "arn:aws:connect:us-west-2:123456789012:instance/00fbeee1-123e-111e-93e3-11111bfbfcc17/security-profile/11dtcggg1-123e-111e-93e3-11111bfbfcc17",
        } 
    ]
}
```