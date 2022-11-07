# Required permissions for using custom IAM policies to manage Cases<a name="required-permissions-iam-cases"></a>

If you're using custom IAM policies to manage access to the Amazon Connect Cases, your users need some or all of the permissions listed in this article, depending on the tasks they need to do\.

## View Cases domain details<a name="view-cases-domain-iam"></a>

There are two options for granting users IAM permissions to view Cases domain details on the Amazon Connect console\.

### Option 1: Minimum required IAM permissions<a name="option1-view-cases-domain-iam"></a>

To view Cases domain details in the Amazon Connect console, users must have the following IAM permissions:
+ `connect:ListInstances`
+ `ds:DescribeDirectories`
+ `connect:ListIntegrationAssociations`
+ `cases:GetDomain`

Following is a sample IAM policy with these permissions:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowsViewingConnectConsole",
            "Effect": "Allow",
            "Action": [
                "connect:ListInstances",
                "ds:DescribeDirectories"
            ],
            "Resource": "*"
        },
        {
            "Sid": "ListIntegrationAssociations",
            "Effect": "Allow",
            "Action": [
                "connect:ListIntegrationAssociations"
            ],
            "Resource": "*"
        },
        {
            "Sid": "CasesGetDomain",
            "Effect": "Allow",
            "Action": [
                "cases:GetDomain"
            ],
            "Resource": "*"
        }
    ]
}
```

Note the following:
+ `cases:GetDomain` Action is required on Resource `*`
+ `connect:ListIntegrationAssociations` action supports the `instance` resource type\. See the table in [Actions defined by Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html#amazonconnect-actions-as-permissions)\.

### Option 2: Update the existing Amazon Connect policy with `cases:GetDomain`<a name="option2-view-cases-domain-iam"></a>

Include the [AmazonConnectReadOnlyAccess](security-iam-amazon-connect-permissions.md#amazonconnectreadonlyaccesspolicy) policy, and add the following `cases:GetDomain` policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CasesGetDomain",
            "Effect": "Allow",
            "Action": [
                "cases:GetDomain"
            ],
            "Resource": "*"
        }
    ]
}
```

## Onboard to Cases<a name="onboard-cases-iam"></a>

There are two options for granting users IAM permissions to onboard to Cases using the Amazon Connect console\.

### Option 1: Minimum required permissions<a name="option1-onboard-cases-iam"></a>

To onboard to Cases by using the Amazon Connect console, users must have the following IAM permissions:
+ `connect:ListInstances`
+ `ds:DescribeDirectories`
+ `connect:ListIntegrationAssociations`
+ `cases:GetDomain`
+ `cases:CreateDomain`
+ `connect:CreateIntegrationAssociation`
+ `connect:DescribeInstance`
+ `iam:PutRolePolicy`

Following is a sample IAM policy with these permissions:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowsViewingConnectConsole",
            "Effect": "Allow",
            "Action": [
                "connect:ListInstances",
                "ds:DescribeDirectories"
            ],
            "Resource": "*"
        },
        {
            "Sid": "ListIntegrationAssociations",
            "Effect": "Allow",
            "Action": [
                "connect:ListIntegrationAssociations"
            ],
            "Resource": "*"
        },
        {
            "Sid": "CasesGetDomain",
            "Effect": "Allow",
            "Action": [
                "cases:GetDomain"
            ],
            "Resource": "*"
        },
        {
            "Sid": "CasesCreateDomain",
            "Effect": "Allow",
            "Action": [
                "cases:CreateDomain"
            ],
            "Resource": "*"
        },
        {
            "Sid": "CreateIntegrationAssociationsAndDependencies",
            "Effect": "Allow",
            "Action": [
                "connect:CreateIntegrationAssociation",
                "connect:DescribeInstance"
            ],
            "Resource": "*"
        },
        {
            "Sid": "AttachAnyPolicyToAmazonConnectRole",
            "Effect": "Allow",
            "Action": "iam:PutRolePolicy",
            "Resource": "arn:aws:iam::*:role/aws-service-role/connect.amazonaws.com/AWSServiceRoleForAmazonConnect*"
        }
    ]
}
```

Note the following:
+ `cases:GetDomain` Action is required on Resource `*`
+ You can scope the permissions to specific Amazon Connect tasks by using the information in [Actions, resources, and condition keys for Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html)\.

### Option 2: Use a combination of existing policies<a name="option2-onboard-cases-iam"></a>

The following combination of policies will also work:
+ **AmazonConnect\_FullAccess** policy
+ `iam:PutRolePolicy` to modify the service\-linked role\. For an example, see [AmazonConnect\_FullAccess policy](security-iam-amazon-connect-permissions.md#amazonconnectfullaccesspolicy)\. 
+ The following IAM policy:

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "CasesGetDomain",
              "Effect": "Allow",
              "Action": [
                  "cases:GetDomain",
                  "cases:CreateDomain"
              ],
              "Resource": "*"
          }
      ]
  }
  ```