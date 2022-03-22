# AWS managed policies for Amazon Connect<a name="security_iam_awsmanpol"></a>

To add permissions to users, groups, and roles, it is more efficient to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) policies that provide your team with only the permissions that they need\. To get started quickly, you can use AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/security-iam-awsmanpol.html) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the ReadOnlyAccess AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AmazonConnect\_FullAccess<a name="AmazonConnect_FullAccess-policy"></a>

To allow full read/write access to Amazon Connect, you must attach two policies to your IAM users, groups, or roles\. Attach the `AmazonConnect_FullAccess` policy and a custom policy with the following contents:

```
{ 
    "Version": "2012-10-17", 
    "Statement": [ 
        { 
            "Sid": "AttachAnyPolicyToAmazonConnectRole", 
            "Effect": "Allow", 
            "Action": "iam:PutRolePolicy", 
            "Resource": "arn:aws:iam::*:role/aws-service-role/connect.amazonaws.com/AWSServiceRoleForAmazonConnect*" 
        } 
    ] 
}
```

To allow an IAM user to create an instance, ensure that they have the permissions granted by the `AmazonConnect_FullAccess` policy\.

When you use `AmazonConnect_FullAccess` policy, note the following:
+ The `iam:PutRolePolicy` allows the user who gets that policy to configure any resource in the account to work with the Amazon Connect instance\. Because it grants such broad permissions, only assign it when necessary\. Instead, create the service\-linked role with access to the necessary resources and let the user have access to pass the service\-linked role to Amazon Connect \(which is granted by the `AmazonConnect_FullAccess` policy\)\. 
+ Additional privileges are required to create a Amazon S3 bucket with a name of your choosing, or use an existing bucket while creating or updating an instance from the Amazon Connect console\. If you choose default storage locations for your call recordings, chat transcripts, call transcripts, etc, they are now prefixed with "amazon\-connect\-"\.
+ The aws/connect KMS key is available to use as a default encryption option\. To use a custom encryption key, assign users additional KMS privileges\.
+ Assign users additional privileges to attach other AWS resources like Amazon Polly, Live Media Streaming, Data Streaming, and Lex bots to their Amazon Connect instances\. 

For more information and detailed permissions, see [Required permissions for using custom IAM policies to manage access to the Amazon Connect console](security-iam-amazon-connect-permissions.md)\. 

## AWS managed policy: AmazonConnectReadOnlyAccess<a name="amazonconnectreadonlyaccesspolicy"></a>

To allow read\-only access, you need to attach only the `AmazonConnectReadOnlyAccess` policy\.

## AWS managed policy: AmazonConnectVoiceIDFullAccess<a name="amazonconnectvoiceidfullaccesspolicy"></a>

To allow full access to Amazon Connect Voice ID, you must attach two policies to your IAM users, groups, or roles\. Attach the `AmazonConnectVoiceIDFullAccess` policy and the following custom policy contents to access Voice ID through the Amazon Connect console: 

```
{ 
    "Version": "2012-10-17", 
    "Statement": [ 
        { 
            "Sid": "AttachAnyPolicyToAmazonConnectRole", 
            "Effect": "Allow", 
            "Action": "iam:PutRolePolicy", 
            "Resource": "arn:aws:iam::*:role/aws-service-role/connect.amazonaws.com/AWSServiceRoleForAmazonConnect*" 
        },
        {
            "Effect": "Allow",
            "Action": [
                "connect:CreateIntegrationAssociation",
                "connect:DeleteIntegrationAssociation",
                "connect:ListIntegrationAssociations"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "events:DeleteRule",
                "events:PutRule",
                "events:PutTargets",
                "events:RemoveTargets"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "events:ManagedBy": "connect.amazonaws.com"
                }
            }
        }
    ] 
}
```

The manual policy configures the following:
+ The `iam:PutRolePolicy` allows the user who gets that policy to configure any resource in the account to work with the Amazon Connect instance\. Because it grants such broad permissions, only assign it when necessary\.
+ To attach a Voice ID domain with an Amazon Connect instance, you need additional Amazon Connect and Amazon EventBridge privileges\. You need privileges to call Amazon Connect APIs to create, delete, and list integration associations\. You need EventBridge permissions to create and delete EventBridge rules which are used to provide contact records related to Voice ID\.

Since there is no default encryption option, to use your customer managed key with your Amazon Connect Voice ID, the following API operations must be permitted in the key policy\. Also, you must add these permissions on the relevant key\. They are not included in the managed policy\.
+ `kms:Decrypt` to access or store encrypted data\.
+ `kms:CreateGrant` – when creating or updating a domain, used to create a grant to the customer managed key for the Voice ID domain\. The grant controls access to the specified KMS key which allows access to [grant operations](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html#terms-grant-operations) Amazon Connect Voice ID requires\. For more information about using grants, see [Using grants](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html) in the *AWS Key Management Service Developer Guide*\.
+ `kms:DescribeKey` – when creating or updating a domain, allows determining the ARN for KMS key you provided\.

For more about creating domains and KMS keys, see [Enable Voice ID](enable-voiceid.md) and [Encryption at rest](encryption-at-rest.md)\. 

## Amazon Connect updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>

View details about updates to AWS managed policies for Amazon Connect since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the [Amazon Connect Document history](doc-history.md) page\. 




| Change | Description | Date | 
| --- | --- | --- | 
|  [AmazonConnectServiceLinkedRolePolicy](connect-slr.md) – Added actions for Amazon CloudWatch  |  Added the following action to publish usage Amazon Connect metrics for an instance to your account\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html)  | Februrary 22, 2022 | 
|  [AmazonConnect\_FullAccess](#AmazonConnect_FullAccess-policy) – Added permissions for managing Amazon Connect Customer Profiles domains  |  Added all permissions for managing Amazon Connect Customer Profiles domains that are created for new Amazon Connect instances\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html) The following permissions are allowed to be performed on domains with a name that is prefixed with `amazon-connect-`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html)  | November 12, 2021 | 
|  [AmazonConnectServiceLinkedRolePolicy](connect-slr.md) – Added actions for Amazon Connect Customer Profiles  |  Added the following actions so Amazon Connect contact flows and the agent experience can interact with the profiles in your default Customer Profiles domain: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html) Added the following action so Amazon Connect contact flows and the agent experience can interact with the profile objects in your default Customer Profiles domain:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html) Added the following action so Amazon Connect contact flows and the agent experience can determine whether Customer Profiles is enabled for your Amazon Connect instance:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html)  | November 12, 2021 | 
|  [AmazonConnectVoiceIDFullAccess](#amazonconnectvoiceidfullaccesspolicy) – Added new AWS managed policy  |  Added a new AWS managed policy so you can set up your users to use Amazon Connect Voice ID\. This policy provides full access to Amazon Connect Voice ID through the AWS console, SDK, or other means\.  | September 27, 2021 | 
|  [AmazonConnectCampaignsServiceLinkedRolePolicy](connect-slr-outbound.md#slr-permissions-outbound) – Added new service\-linked role policy  |  Added a new service\-linked role policy for Amazon Connect High\-Volume Outbound Communications\. The policy provides access to retrieve all the high\-volume outbound campaigns\.  | September 27, 2021 | 
|  [AmazonConnectServiceLinkedRolePolicy](connect-slr.md) – Added actions for Amazon Lex  |  Added the following actions for the all bots created in the account across all Regions\. These actions were added to support integration with Amazon Lex\.  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html)  | June 15, 2021 | 
| [AmazonConnect\_FullAccess](security-iam-amazon-connect-permissions.md) – Added actions for Amazon Lex   |  Added the following actions for the all bots created in the account across all Regions\. These actions were added to support integration with Amazon Lex\.  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security_iam_awsmanpol.html)  | June 15, 2021 | 
|  Amazon Connect started tracking changes  |  Amazon Connect started tracking changes for its AWS managed policies\.  | June 15, 2021 | 