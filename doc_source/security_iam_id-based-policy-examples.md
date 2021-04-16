# Amazon Connect identity\-based policy examples<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify Amazon Connect resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform specific API operations on the specified resources they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using these example JSON policy documents, see [Creating Policies on the JSON Tab](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor) in the *IAM User Guide*\.

**Topics**
+ [Policy best practices](#security_iam_service-with-iam-policy-best-practices)
+ [Allow IAM users to view their own permissions](#security_iam_id-based-policy-examples-view-own-permissions)
+ [Grant "View User" permissions](#security_iam_id-based-policy-example-view-user-permissions)
+ [Allow IAM users to integrate with external applications](#security_iam_id-based-policy-examples-integrate)
+ [Describe and update Amazon Connect users based on tags](#security_iam_id-based-policy-examples-view-widget-tags)
+ [Create Amazon Connect users based on tags](#connect-access-control-resources-example1)
+ [Create and view Amazon AppIntegrations resources](#appintegration-resources-example1)

## Policy best practices<a name="security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies are very powerful\. They determine whether someone can create, access, or delete Amazon Connect resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started using AWS managed policies** – To start using Amazon Connect quickly, use AWS managed policies to give your employees the permissions they need\. These policies are already available in your account and are maintained and updated by AWS\. For more information, see [Get started using permissions with AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies) in the *IAM User Guide*\.
+ **Grant least privilege** – When you create custom policies, grant only the permissions required to perform a task\. Start with a minimum set of permissions and grant additional permissions as necessary\. Doing so is more secure than starting with permissions that are too lenient and then trying to tighten them later\. For more information, see [Grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.
+ **Enable MFA for sensitive operations** – For extra security, require IAM users to use multi\-factor authentication \(MFA\) to access sensitive resources or API operations\. For more information, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.
+ **Use policy conditions for extra security** – To the extent that it's practical, define the conditions under which your identity\-based policies allow access to a resource\. For example, you can write conditions to specify a range of allowable IP addresses that a request must come from\. You can also write conditions to allow requests only within a specified date or time range, or to require the use of SSL or MFA\. For more information, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

## Allow IAM users to view their own permissions<a name="security_iam_id-based-policy-examples-view-own-permissions"></a>

This example shows how you might create a policy that allows IAM users to view the inline and managed policies that are attached to their user identity\. This policy includes permissions to complete this action on the console or programmatically using the AWS CLI or AWS API\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ViewOwnUserInfo",
            "Effect": "Allow",
            "Action": [
                "iam:GetUserPolicy",
                "iam:ListGroupsForUser",
                "iam:ListAttachedUserPolicies",
                "iam:ListUserPolicies",
                "iam:GetUser"
            ],
            "Resource": ["arn:aws:iam::*:user/${aws:username}"]
        },
        {
            "Sid": "NavigateInConsole",
            "Effect": "Allow",
            "Action": [
                "iam:GetGroupPolicy",
                "iam:GetPolicyVersion",
                "iam:GetPolicy",
                "iam:ListAttachedGroupPolicies",
                "iam:ListGroupPolicies",
                "iam:ListPolicyVersions",
                "iam:ListPolicies",
                "iam:ListUsers"
            ],
            "Resource": "*"
        }
    ]
}
```

## Grant "View User" permissions<a name="security_iam_id-based-policy-example-view-user-permissions"></a>

When you create an IAM user or [group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html#id_iam-groups) in your AWS account, you can associate an IAM policy with that group or user, which specifies the permissions that you want to grant\.

For example, imagine you have a group of entry\-level developers\. You can create an IAM group named `Junior application developers`, and include all entry\-level developers\. Then, associate a policy with that group that grants them permissions to view Amazon Connect users\. In this scenario, you might have a policy such as the following sample\. 

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

## Allow IAM users to integrate with external applications<a name="security_iam_id-based-policy-examples-integrate"></a>

This example shows how you might create a policy that allows IAM users to interact with their external application integrations\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAllAppIntegrationsActions",
            "Effect": "Allow",
            "Action": [
                "app-integrations:ListEventIntegrations",
                "app-integrations:CreateEventIntegration",
                "app-integrations:GetEventIntegration",
                "app-integrations:UpdateEventIntegration",
                "app-integartions:DeleteEventIntegration"
            ],
            "Resource": "*" 
	}
	]
}
```

## Describe and update Amazon Connect users based on tags<a name="security_iam_id-based-policy-examples-view-widget-tags"></a>

In an IAM policy, you can optionally specify conditions that control when a policy is in effect\. For example, you can define a policy that allows IAM users to update only an Amazon Connect user who is working in the test environment\.

You can define some conditions that are specific to Amazon Connect, and define other conditions that apply to all of AWS\. For more information and a list of AWS\-wide conditions, see Condition in [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\. 

The following sample policy allows the "describe" and "update" actions for users with specific tags\.

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

## Create Amazon Connect users based on tags<a name="connect-access-control-resources-example1"></a>

The following sample policy allows the create actions for users with specific request tags\.

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

## Create and view Amazon AppIntegrations resources<a name="appintegration-resources-example1"></a>

The following sample policy allows event integrations to be created, listed, and fetched\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "app-integrations:CreateEventIntegration",
                "app-integrations:GetEventIntegration",
                "app-integrations::ListEventIntegrations",
            ],
            "Resource": "*"
        }
    ]
}
```