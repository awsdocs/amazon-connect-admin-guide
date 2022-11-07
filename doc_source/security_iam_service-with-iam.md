# How Amazon Connect works with IAM<a name="security_iam_service-with-iam"></a>

Before you use IAM to manage access to Amazon Connect, you should understand what IAM features are available to use with Amazon Connect\. To get a high\-level view of how Amazon Connect and other AWS services work with IAM, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [Amazon Connect identity\-based policies](#security_iam_service-with-iam-id-based-policies)
+ [Authorization based on Amazon Connect tags](#security_iam_service-with-iam-tags)
+ [Amazon Connect IAM roles](#security_iam_service-with-iam-roles)

## Amazon Connect identity\-based policies<a name="security_iam_service-with-iam-id-based-policies"></a>

With IAM identity\-based policies, you can specify allowed or denied actions and resources as well as the conditions under which actions are allowed or denied\. Amazon Connect supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Action` element of a JSON policy describes the actions that you can use to allow or deny access in a policy\. Policy actions usually have the same name as the associated AWS API operation\. There are some exceptions, such as *permission\-only actions* that don't have a matching API operation\. There are also some operations that require multiple actions in a policy\. These additional actions are called *dependent actions*\.

Include actions in a policy to grant permissions to perform the associated operation\.

Policy actions in Amazon Connect use the following prefix before the action: `connect:`\.  Policy statements must include either an `Action` or `NotAction` element\. Amazon Connect defines its own set of actions that describe tasks that you can perform with this service\.

To specify multiple actions in a single statement, separate them with commas as follows:

```
"Action": [
      "connect:action1",
      "connect:action2"
```

You can specify multiple actions using wildcards \(\*\)\. For example, to specify all actions that begin with the word `Describe`, include the following action:

```
"Action": "connect:Describe*"
```

To see a list of Amazon Connect actions, [Actions, Resources, and Condition Keys for Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html)\.

### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

Amazon Connect supports resource\-level permissions \(specifying a resource ARN in an IAM policy\)\. Following is a list of Amazon Connect resources:
+ Instance
+ Contact
+ User
+ Routing profile
+ Security profile
+ Hierarchy group
+ Queue
+ Flow
+ Hours of operation
+ Phone number
+ Task templates
+ Customer profile domain
+ Customer profile object type
+ Outbound campaigns

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Resource` JSON policy element specifies the object or objects to which the action applies\. Statements must include either a `Resource` or a `NotResource` element\. As a best practice, specify a resource using its [Amazon Resource Name \(ARN\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\. You can do this for actions that support a specific resource type, known as *resource\-level permissions*\.

For actions that don't support resource\-level permissions, such as listing operations, use a wildcard \(\*\) to indicate that the statement applies to all resources\.

```
"Resource": "*"
```

The Amazon Connect instance resource has the following ARN:

```
arn:${Partition}:connect:${Region}:${Account}:instance/${InstanceId}
```

For more information about the format of ARNs, see [Amazon Resource Names \(ARNs\) and AWS Service Namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\.

For example, to specify the `i-1234567890abcdef0` instance in your statement, use the following ARN:

```
"Resource": "arn:aws:connect:us-east-1:123456789012:instance/i-1234567890abcdef0"
```

To specify all instances that belong to a specific account, use the wildcard \(\*\):

```
"Resource": "arn:aws:connect:us-east-1:123456789012:instance/*"
```

Some Amazon Connect actions, such as those for creating resources, cannot be performed on a specific resource\. In those cases, you must use the wildcard \(\*\)\.

```
"Resource": "*"
```

Many Amazon Connect; API actions involve multiple resources\. For example,

To specify multiple resources in a single statement, separate the ARNs with commas\. 

```
"Resource": [
      "resource1",
      "resource2"
```

To see a list of Amazon Connect resource types and their ARNs, see [Actions, Resources, and Condition Keys for Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html)\. The same article explains with which actions you can specify the ARN of each resource\.

### Condition keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Condition` element \(or `Condition` *block*\) lets you specify conditions in which a statement is in effect\. The `Condition` element is optional\. You can create conditional expressions that use [condition operators](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html), such as equals or less than, to match the condition in the policy with values in the request\. 

If you specify multiple `Condition` elements in a statement, or multiple keys in a single `Condition` element, AWS evaluates them using a logical `AND` operation\. If you specify multiple values for a single condition key, AWS evaluates the condition using a logical `OR` operation\. All of the conditions must be met before the statement's permissions are granted\.

 You can also use placeholder variables when you specify conditions\. For example, you can grant an IAM user permission to access a resource only if it is tagged with their IAM user name\. For more information, see [IAM policy elements: variables and tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_variables.html) in the *IAM User Guide*\. 

AWS supports global condition keys and service\-specific condition keys\. To see all AWS global condition keys, see [AWS global condition context keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.

Amazon Connect defines its own set of condition keys and also supports using some global condition keys\. To see all AWS global condition keys, see [AWS Global Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.

All Amazon EC2 actions support the `aws:RequestedRegion` and `ec2:Region` condition keys\. For more information, see [Example: Restricting Access to a Specific Region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ExamplePolicies_EC2.html#iam-example-region)\. 

To see a list of Amazon Connect condition keys, see [Actions, Resources, and Condition Keys for Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html)\.

### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>

To view examples of Amazon Connect identity\-based policies, see [Amazon Connect identity\-based policy examples](security_iam_id-based-policy-examples.md)\.

## Authorization based on Amazon Connect tags<a name="security_iam_service-with-iam-tags"></a>

You can attach tags to Amazon Connect resources or pass tags in a request to Amazon Connect\. To control access based on tags, you provide tag information in the [condition element](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) of a policy using the `connect:ResourceTag/key-name`, `aws:RequestTag/key-name`, or `aws:TagKeys` condition keys\. 

To view an example identity\-based policy for limiting access to a resource based on the tags on that resource, see [Describe and update Amazon Connect users based on tags](security_iam_id-based-policy-examples.md#security_iam_id-based-policy-examples-view-widget-tags)\.

## Amazon Connect IAM roles<a name="security_iam_service-with-iam-roles"></a>

An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an entity within your AWS account that has specific permissions\.

### Using temporary credentials with Amazon Connect<a name="security_iam_service-with-iam-roles-tempcreds"></a>

You can use temporary credentials to sign in with federation, assume an IAM role, or to assume a cross\-account role\. You obtain temporary security credentials by calling AWS STS API operations such as [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) or [GetFederationToken](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetFederationToken.html)\. 

Amazon Connect supports using temporary credentials\. 

### Service\-linked roles<a name="security_iam_service-with-iam-roles-service-linked"></a>

[Service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role) allow AWS services to access resources in other services to complete an action on your behalf\. Service\-linked roles appear in your IAM account and are owned by the service\. An IAM administrator can view but not edit the permissions for service\-linked roles\.

Amazon Connect supports service\-linked roles\. For details about creating or managing Amazon Connect service\-linked roles, see [Use service\-linked roles for Amazon Connect](connect-slr.md)\. 

### Choosing an IAM role in Amazon Connect<a name="security_iam_service-with-iam-roles-choose"></a>

When you create a resource in Amazon Connect, you must choose a role to allow Amazon Connect to access Amazon EC2 on your behalf\. If you have previously created a service role or service\-linked role, then Amazon Connect provides you with a list of roles to choose from\. It's important to choose a role that allows access to start and stop Amazon EC2 instances\. 