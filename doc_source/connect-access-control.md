# Controlling Access with AWS Identity and Access Management<a name="connect-access-control"></a>

AWS Identity and Access Management \(IAM\) is a web service that helps you securely control access to AWS resources\. For people who access Amazon Connect APIs, you can create [IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html#id_iam-users)\. This enables you to manage at a granular level what these users can do with Amazon Connect, such as whether they can create or delete an instance\. 

You can also manage what other AWS services and resources are available to each IAM user\. For more information about all the services that you can control access to, see [AWS Services that Support IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

## Amazon Connect Actions<a name="connect-access-control-actions"></a>

When you create an IAM user or [group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html#id_iam-groups) in your AWS account, you can associate an IAM policy with that group or user, which specifies the permissions that you want to grant\.

For example, imagine you have a group of entry\-level developers\. You can create an IAM group named `Junior application developers`, and include all entry\-level developers\. Then, associate a policy with that group that grants them permissions to view Amazon Connect users\. In this scenario, you might have a policy such as the following sample\. 

### Sample policy that grants "view user" permissions to IAM users<a name="connect-access-control-actions-sample1"></a>

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "connect:DescribeUser",
                "connect:ListUsers"
            ],
            "Resource": "*"
        }
    ]
}
```

This sample policy grants permissions to API actions listed in the `Action` element\.

**Note**  
If you don't specify a user ARN or ID in your statement, you must also grant the permission to use all resources for the action using the \* wildcard for the `Resource` element\.

## Amazon Connect Resources<a name="connect-access-control-resources"></a>

Amazon Connect supports resource\-level permissions for IAM users, so you can specify actions for them for an instance, as shown in the following policy\.

### Sample policy that denies the "delete" and "update" actions for users in one instance<a name="connect-access-control-resources-example1"></a>

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

This sample policy uses a wild card at the end of the Amazon Connect user ARN so that "delete user" and "update user" are denied on the full user ARN \(that is, all Amazon Connect users in the provided instance, such as arn:aws:connect:us\-east\-1:123456789012:instance/00fbeee1\-123e\-111e\-93e3\-11111bfbfcc1/agent/00dtcddd1\-123e\-111e\-93e3\-11111bfbfcc1\)\.

### Sample policy that allows "create users" but denies if you're assigned to a specific security profile<a name="connect-access-control-resources-example2"></a>

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

This sample policy allows "create users" but explicitly denies using arn:aws:connect:us\-west\-2:123456789012:instance/00fbeee1\-123e\-111e\-93e3\-11111bfbfcc1/security\-profile/11dtcggg1\-123e\-111e\-93e3\-11111bfbfcc17 as the parameter for security profile in [CreateUser](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateUser.html#API_CreateUser_RequestBody) request\.

## Amazon Connect Conditions<a name="connect-access-control-conditions"></a>

In an IAM policy, you can optionally specify conditions that control when a policy is in effect\. For example, you can define a policy that allows IAM users to update only an Amazon Connect user who is working in the test environment\.

You can define some conditions that are specific to Amazon Connect, and define other conditions that apply to all of AWS\. For more information and a list of AWS\-wide conditions, see Condition in [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\. 

### Sample policy that allows the "describe" and "update" actions for users with specific tags<a name="connect-access-control-conditions-example1"></a>

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "connect:DescribeUser",
                "connect:UpdateUser*"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/Department": "Test"
                }
            }            
        }
    ]
}
```

This policy allows "describe user" and "update user" but only for those Amazon Connect users tagged with tag “Department: Test” where “Department” is the tag key and “Test” is the tag value\. 

### Sample policy that allows the create actions for users with specific request tags<a name="connect-access-control-resources-example2"></a>

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "connect:CreateUser",
                "connect:TagResource"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestTag/Owner": "TeamA"
                }
            }
        }
    ]
}
```

This policy allows "create user" and "tag resource" but the tag “Owner: TeamA” must be present in the requests\.