# Cross\-service confused deputy prevention<a name="cross-service-confused-deputy-prevention"></a>

The confused deputy problem is a security issue where an entity that doesn't have permission to perform an action can coerce a more\-privileged entity to perform the action\. In AWS, cross\-service impersonation can result in the confused deputy problem\. Cross\-service impersonation can occur when one service \(the *calling service*\) calls another service \(the *called service*\)\. The calling service can be manipulated to use its permissions to act on another customer's resources in a way it should not otherwise have permission to access\. To prevent this, AWS provides tools that help you protect your data for all services with service principals that have been given access to resources in your account\. 

We recommend using the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys in resource policies to limit the permissions that Amazon Connect gives another service to the resource\. If you use both global condition context keys, the `aws:SourceAccount` value and the account in the `aws:SourceArn` value must use the same account ID when used in the same policy statement\.

The most effective way to protect against the confused deputy problem is to use the exact Amazon Resource Name \(ARN\) of the resource you want to allow\. If you don't know the full ARN of the resource or if you are specifying multiple resources, use the `aws:SourceArn` global context condition key with wildcards \(`*`\) for the unknown portions of the ARN\. For example, `arn:aws:servicename::region-name::your AWS account ID:*`\.

## Amazon Connect Customer Profiles cross\-service confused deputy prevention<a name="customer-profiles-cross-service"></a>

The following examples show policies that apply to cases where someone else is set up as the administrator for Amazon Connect Customer Profiles\. Use these policies to prevent the confused deputy problem\.

**Example Amazon Connect Customer Profiles policy to create Customer Profile domains**

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Sid": "ConfusedDeputyPreventionExamplePolicy",
    "Effect": "Allow",
    "Principal": {
      "Service": "profile.amazonaws.com"
    },
    "Action": ["kms:GenerateDataKey", "kms:CreateGrant", "kms:Decrypt"],
    "Resource": [
      "arn:aws:kms:your region-name:your AWS account ID:key/your key ARN"
    ],
    "Condition": {
      "ArnEquals": {
        "aws:SourceArn": "arn:aws:profile:your region name:your AWS account ID:domains/your Customer Profiles domain name"
      },
      "StringEquals": {
        "aws:SourceAccount": "your AWS account ID"
      }
    }
  }
}
```

**Example Amazon Connect Customer Profiles policy to create Customer Profiles object types**

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Sid": "ConfusedDeputyPreventionExamplePolicy",
    "Effect": "Allow",
    "Principal": {
      "Service": "profile.amazonaws.com"
    },
    "Action": ["kms:GenerateDataKey", "kms:CreateGrant", "kms:Decrypt"],
    "Resource": [
      "arn:aws:kms:your Region:your AWS account ID:key/your key ARN"
    ],
    "Condition": {
      " ArnEquals": {
        "aws:SourceArn": "arn:aws:profile:your region name:your AWS account ID:domains/your Customer Profiles domain name/objects/your object type"
      },
      "StringEquals": {
        "aws:SourceAccount": "your AWS account ID"
      }
    }
  }
}
```

**Example Amazon Connect Customer Profiles policy to create and update dead\-letter queues**

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow Amazon Connect Customer Profiles to publish messages to your queue",
      "Effect": "Allow",
      "Principal": {
        "Service": "profile.amazonaws.com"
      },
      "Action": "sqs:SendMessage",
      "Resource": "your dead-letter queue ARN",

      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "your AWS account ID",
          "aws:SourceArn": "arn:aws:profile:your region name:your AWS account ID:domains/your Customer Profiles domain name"
        }
      }
    }
  ]
}
```

**Example Amazon Connect Customer Profiles policy to protect the Amazon S3 bucket used as part of the Identity Resolution process**

```
{
    "Sid": "Allow Amazon Connect Customer Profiles to put S3 objects to your bucket",
    "Effect": "Allow",
    "Principal": {
        "Service": "profile.amazonaws.com"
    },
    "Action": "s3:PutObject",
    "Resource": "arn:aws:s3:::your S3 bucket name/*",
    "Condition": {
        "StringEquals": {
            "aws:SourceAccount": "your AWS account ID"
        },
        "ArnEquals": {
            "aws:SourceArn": "arn:aws:profile:your region name:your AWS account ID:domains/*"
        }
    }
}
```

## Amazon Connect Voice ID cross\-service confused deputy prevention<a name="voiceid-cross-service"></a>

The following Voice ID example shows a resource policy to apply to prevent the confused deputy problem\.

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Sid": "ConfusedDeputyPreventionExamplePolicy",
    "Effect": "Allow",
    "Principal": {
      "Service": "voiceid.amazonaws.com"
    },
    "Action": "sts:AssumeRole",
    "Condition": {
      "ArnEquals": {
        "aws:SourceArn": "arn:aws:voiceid:your region name:your AWS account ID:domain/your Voice ID domain name"
      },
      "StringEquals": {
        "aws:SourceAccount": "your AWS account ID"
      }
    }
  }
}
```

## Amazon Connect chat message streaming cross\-service confused deputy prevention<a name="connect-message-streaming-cross-service"></a>

The following Amazon Connect example shows a resource policy to apply to prevent the confused deputy problem\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"connect.amazonaws.com"
         },
         "Action":"sns:Publish",
         "Resource":"your SNS topic ARN",
         "Condition":{
            "StringEquals":{
               "aws:SourceAccount":"your AWS account ID"
            },
            "ArnEquals":{
               "aws:SourceArn":"your Amazon Connect instance ARN"
            }
         }
      }
   ]
}
```