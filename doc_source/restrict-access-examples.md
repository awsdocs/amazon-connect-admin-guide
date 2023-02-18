# Restrict AWS resources that can be associated with Amazon Connect<a name="restrict-access-examples"></a>

Each Amazon Connect instance is associated with an IAM [ service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role) when the instance is created\. Amazon Connect can integrate with other AWS services for use cases such as call recording storage \(Amazon S3 bucket\), natural language bots \(Amazon Lex bots\), and data streaming \(Amazon Kinesis Data Streams\)\. Amazon Connect assumes the service\-linked role to interact with these other services\. The policy is first added to the service\-linked role as part of corresponding APIs on the Amazon Connect service \(that are in turn called by the AWS console\)\. For example, if you want to use a certain Amazon S3 bucket with your Amazon Connect instance, the bucket must be passed to the [ AssociateInstanceStorageConfig](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociateInstanceStorageConfig.html) API\.

For the set of IAM actions defined by Amazon Connect, see [Actions defined by Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html#amazonconnect-actions-as-permissions)\.

Following are some examples of how to restrict access to other resources that may be associated with an Amazon Connect instance\. They should be applied to the User or Role that is interacting with Amazon Connect APIs or the Amazon Connect console\. 

**Note**  
A policy with an explicit `Deny` would override the `Allow` policy in these examples\.

For more information about what resources, condition keys, and dependent APIs you can use to restrict access, see [Actions, resources, and condition keys for Amazon Connect](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonconnect.html)\. 

## Example 1: Restrict which Amazon S3 buckets can be associated with an Amazon Connect instance<a name="example1-restrict-buckets"></a>

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": [
        "connect:UpdateInstanceStorageConfig",
        "connect:AssociateInstanceStorageConfig"
      ],
      "Resource": "arn:aws:connect:region:account-id:instance/instance-id",
      "Condition": {
        "StringEquals": {
          "connect:StorageResourceType": "CALL_RECORDINGS"
        }
      }
    },
    {
      "Sid": "VisualEditor1",
      "Effect": "Allow",
      "Action": [
        "iam:PutRolePolicy",
        "s3:GetBucketAcl",
        "s3:GetBucketLocation"
      ],
      "Resource": [
        "arn:aws:iam::account-id:role/aws-service-role/connect.amazonaws.com/*",
        "arn:aws:s3:::s3-bucket-name"
      ]
    },
    {
      "Sid": "VisualEditor2",
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    }
  ]
}
```

This example allows an IAM principal to associate an Amazon S3 bucket for call recordings for the given Amazon Connect instance ARN, and a specific Amazon S3 bucket named `my-connect-recording-bucket`\. The `AttachRolePolicy` and `PutRolePolicy `actions are scoped to the Amazon Connect service\-linked role \(a wildcard is used in this example, but you can provide the role ARN for the instance if needed\)\.

**Note**  
To use an AWS KMS key to encrypt recordings in this bucket, an additional policy is needed\. 

## Example 2: Restrict which AWS Lambda functions can be associated with an Amazon Connect instance<a name="example2-restrict-lambda-functions"></a>

AWS Lambda functions are associated with an Amazon Connect instance, but the Amazon Connect service\-linked role is not used to invoke them, and so is not modified\. Instead, a policy is added to the function through the `lambda:AddPermission` API that allows the given Amazon Connect instance to invoke the function\. 

To restrict which functions can be associated with an Amazon Connect instance, you specify the Lambda function ARN that a user can use to invoke `lambda:AddPermission`: 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "connect:AssociateLambdaFunction",
                "lambda:AddPermission"
            ],
            "Resource": [
                "arn:aws:connect:region:account-id:instance/instance-id",
                "arn:aws:lambda:*:*:function:my-function"      
            ]
        }
    ]
}
```

## Example 3: Restrict which Amazon Kinesis Data Streams can be associated with an Amazon Connect instance<a name="example3-restrict-kinesis-data-streams"></a>

This example follows a similar model to the Amazon S3 example\. It restricts which specific Kinesis Data Streams may be associated with a given Amazon Connect instance for delivering contact records\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "connect:UpdateInstanceStorageConfig",
                "connect:AssociateInstanceStorageConfig"
            ],
            "Resource": "arn:aws:connect:region:account-id:instance/instance-id",
            "Condition": {
                "StringEquals": {
                    "connect:StorageResourceType": "CONTACT_TRACE_RECORDS"
                }
            }
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "kinesis:DescribeStream",
                "iam:PutRolePolicy"
            ],
            "Resource": [
                "arn:aws:iam::account-id:role/aws-service-role/connect.amazonaws.com/*",
                "arn:aws:kinesis:*:account-id:stream/stream-name"
            ]
        }, 
        {
            "Sid": "VisualEditor2",
            "Effect": "Allow",
            "Action":  "kinesis:ListStreams",
            "Resource": "*"            
        }
    ]
}
```