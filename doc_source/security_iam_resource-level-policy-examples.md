# Amazon Connect resource\-level policy examples<a name="security_iam_resource-level-policy-examples"></a>

Amazon Connect supports resource\-level permissions for IAM users, so you can specify actions for them for an instance, as shown in the following policies\.

## Deny the "delete" and "update" actions<a name="connect-access-control-resources-example2"></a>

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

## Allow actions for integrations with specific names<a name="connect-access-control-resources-integration-example"></a>

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
"Resource":"arn:aws:appintegrations:*:*:event-integration/MyNamePrefix-*"
	}
    ]
}
```

## Allow "create users" but deny if you're assigned to a specific security profile<a name="connect-access-control-resources-example3"></a>

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

## Allow recording actions on a contact<a name="connect-access-control-resources-example4"></a>

The following sample policy allows "start contact recording" on a contact in a specific instance\. Since contactID is dynamic, \* is used\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
          "connect:StartContactRecording"
      ],
      "Resource": "arn:aws:connect:us-west-2:accountID:instance/instanceId/contact/*",
      "Effect": "Allow"
    }
  ]
}
```

Set up a trusted relationship with *accountID*\.

The following actions are defined for the recording APIs:
+ "connect:StartContactRecording"
+ "connect:StopContactRecording"
+ "connect:SuspendContactRecording"
+ "connect:ResumeContactRecording"

### Allow more contact Actions in the same role<a name="example4-allow-more-actions"></a>

If the same role is used to calling other contact APIs, you can list the following contact actions:
+ GetContactAttributes
+ ListContactFlows
+ StartChatContact
+ StartOutboundVoiceContact
+ StopContact
+ UpdateContactAttributes

Or use a wildcard to allow all contact actions, for example: "connect:\*"

### Allow more resources<a name="example4-allow-more-resources"></a>

You can also use a wildcard to allow more resources\. For example, here's how to allow contact actions on all contact resources:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "connect:*"
            ],
            "Resource": "arn:aws:connect:us-west-2:accountID:instance/*/contact/*",
            "Effect": "Allow"
        }
    ]
}
```

## View specific Amazon AppIntegrations resources<a name="view-specific-appintegrations-resources"></a>

The following sample policy allows a specific event integrations to be fetched\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "app-integrations:GetEventIntegration"
            ],
            "Resource": "arn:aws:app-integrations:us-west-2:accountID:event-integration/Name"
        }
    ]
}
```

## Grant access to Amazon Connect Customer Profiles<a name="grant-access-to-customer-profiles"></a>

Amazon Connect Customer Profiles use `profile` as the prefix for actions instead of `connect`\. The following policy grants full access to a specific domain in Amazon Connect Customer Profiles\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
          "profile:*"
      ],
      "Resource": "arn:aws:profile:us-west-2:accountID:domains/domainName",
      "Effect": "Allow"
    }
  ]
}
```

Set up a trusted relationship with accountID to domain domainName\.

## Grant read\-only access to Customer Profiles data<a name="grant-read-only-access-to-customer-profiles"></a>

Following is an example for granting read access to the data in Amazon Connect Customer Profiles\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "profile:SearchProfiles",
                "profile:ListObjects"
            ],
            "Resource": "arn:aws:profile:us-west-2:accountID:domains/domainName",
            "Effect": "Allow"
        }
    ]
}
```