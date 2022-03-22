# Encryption at rest<a name="encryption-at-rest"></a>

Contact data classified as PII, or data that represents customer content being stored by Amazon Connect, is encrypted at rest \(that is, before it is put, stored, or saved to a disk\) using a key that is time\-limited and specific to the Amazon Connect instance\.

Amazon S3 server\-side encryption is used to encrypt conversation recordings \(voice and chat\) and knowledge documents at rest with a AWS Key Management Service data key unique per customer account\. Amazon AppIntegrations configuration data is encrypted the same way\. For information about AWS KMS keys, see [What is AWS Key Management Service?](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\.

Amazon Connect Voice ID stores customer voiceprints which cannot be reverse\-engineered to obtain the enrolled customer’s speech or identify a customer\. These are encrypted using a service\-owned AWS KMS key\.

Integration configuration data is encrypted at rest using a key that is time\-limited and specific to the user account\.

## External application data encryption at rest<a name="encryption-at-rest-appintegrations"></a>

When you create a DataIntegration encrypted with a customer managed key, Amazon AppIntegrations creates a grant on your behalf by sending a `CreateGrant` request to AWS KMS\. Grants in AWS KMS are used to give Amazon AppIntegrations access to a KMS key in your account\. 

You can revoke access to the grant, or remove the access that Amazon AppIntegrations has to the customer managed key at any time\. If you do, Amazon AppIntegrations can not access any of the data encrypted by the customer managed key, which affects operations that are dependent on that data\. 

External application data that Amazon AppIntegrations processes is encrypted at rest in an S3 bucket using the customer managed key that you provided during configuration\.

Amazon AppIntegrations requires the grant to use the customer managed key for the following internal operations:
+ Send `GenerateDataKeyRequest` to AWS KMS to generate data keys encrypted by your customer managed key\.
+ Send `Decrypt` requests to AWS KMS to decrypt encrypted data keys so that they can be used to encrypt your data\.

## Amazon Connect Customer Profiles encryption at rest<a name="encryption-at-rest-customer-profiles"></a>

All user data stored in Amazon Connect Customer Profiles is encrypted at rest\. Amazon Connect Customer Profiles encryption at rest provides enhanced security by encrypting all your data at rest using encryption keys stored in AWS Key Management Service \(AWS KMS\)\. This functionality helps reduce the operational burden and complexity involved in protecting sensitive data\. With encryption at rest, you can build security\-sensitive applications that meet strict encryption compliance and regulatory requirements\.

Organizational policies, industry or government regulations, and compliance requirements often require the use of encryption at rest to increase the data security of your applications\. Customer Profiles integrated with AWS KMS to enable its encryption at rest strategy\. For more information, see [AWS Key Management Service Concepts](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html) in the AWS Key Management Service Developer Guide\. 

When creating a new domain, you must provide a [KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#kms_keys) that the service will use to encrypt your data in transit and at rest\. The customer managed key is created, owned, and managed by you\. You have full control over the customer managed key \(AWS KMS charges apply\)\.

You can specify an encryption key when you create a new domain or profile object type or switch the encryption keys on an existing resources by using the AWS Command Line Interface \(AWS CLI\), or the Amazon Connect Customer Profiles Encryption API\. When you choose a customer managed key, Amazon Connect Customer Profiles creates a grant to the customer managed key that grants it access to the customer managed key\.

AWS KMS charges apply for a customer managed key\. For more information about pricing, see [AWS KMS pricing](http://aws.amazon.com/kms/pricing/)\. 

## Amazon Connect Wisdom encryption at rest<a name="encryption-at-rest-wisdom"></a>

All user data stored in Amazon Connect Wisdom is encrypted at rest using encryption keys stored in AWS Key Management Service\. If you optionally provide a customer managed key, Wisdom uses it to encrypt knowledge content stored at rest outside of Wisdom search indices\. Wisdom uses dedicated search indices per customer and they are encrypted at rest by using AWS owned keys stored in AWS Key Management Service\. Additionally, you can use CloudTrail to audit any data access via the Wisdom APIs\.

AWS KMS charges apply when using a key that you provide\. For more information about pricing, see [AWS KMS pricing](http://aws.amazon.com/kms/pricing/)\.

## Amazon Connect Voice ID encryption at rest<a name="encryption-at-rest-voiceid"></a>

All user data stored in Amazon Connect Voice ID is encrypted at rest\. When creating a new Voice ID domain, you must provide a customer managed key that the service uses to encrypt your data at rest\. The customer managed key is created, owned, and managed by you\. You have full control over the key\.

You can update the KMS key in the Voice ID domain by using the update\-domain command in AWS Command Line Interface \(AWS CLI\), or the [UpdateDomain](https://docs.aws.amazon.com/voiceid/APIReference/API_UpdateDomain.html) Voice ID API\. Note that updating the KMS key changes the key used to encrypt new data added after updating the key, and not the key that was used to encrypt the old data\.

Voice ID creates a grant to the customer managed key that grants it access to the key\. For more information, see [How Amazon Connect Voice ID uses grants in AWS KMS](#voiceid-uses-grants)\. 

Following is a list of data that is encrypted at rest using the customer managed key:
+ **Voiceprints**: The voiceprints generated while enrolling the speakers and registering fraudsters into the system\.
+ **Speaker and fraudster audio**: The audio data used for enrolling the speakers and registering the fraudsters\.
+ **CustomerSpeakerId**: The customer\-provided SpeakerId while enrolling the customer into Voice ID\. 
+ **Customer\-provided metadata**: These include free\-form strings such as `Domain` `Description`, `Domain Name`, `Job Name`, and more\.

AWS KMS charges apply for a customer managed key\. For more information about pricing, see [AWS KMS pricing](http://aws.amazon.com/kms/pricing/)\. 

### How Amazon Connect Voice ID uses grants in AWS KMS<a name="voiceid-uses-grants"></a>

Amazon Connect Voice ID requires a grant to use your customer managed key\. When you create a domain, Voice ID creates a grant on your behalf by sending a see [CreateGrant](https://docs.aws.amazon.com/kms/latest/APIReference/API_CreateGrant.html) request to AWS KMS\. The grant is required to use your customer managed key for the following internal operations:
+ Send [DescribeKey](https://docs.aws.amazon.com/kms/latest/APIReference/API_DescribeKey.html) requests to AWS KMS to verify that the symmetric customer managed key ID provided is valid\. 
+ Send [GenerateDataKey](https://docs.aws.amazon.com/kms/latest/APIReference/API_GenerateDataKey.html) requests to KMS key to create data keys with which to encrypt objects\.
+ Send [Decrypt](https://docs.aws.amazon.com/kms/latest/APIReference/API_Decrypt.html) requests to AWS KMS to decrypt the encrypted data keys so that they can be used to encrypt your data\. 
+ Send [ReEncrypt](https://docs.aws.amazon.com/kms/latest/APIReference/API_ReEncrypt.html) requests to AWS KMS when the key is updated to re\-encrypt a limited set of data using the new key\.
+ Store files in S3 using the AWS KMS key to encrypt the data\.

You can revoke access to the grant, or remove the service's access to the customer managed key at any time\. If you do, Voice ID won't be able to access any of the data encrypted by the customer managed key, which affects all the operations that are dependent on that data, leading to `AccessDeniedException` errors and failures in the asynchronous workflows\.

### Customer managed key policy for Voice ID<a name="encryption-at-rest-cmkpolicy-voiceid"></a>

Key policies control access to your customer managed key\. Every customer managed key must have exactly one key policy, which contains statements that determine who can use the key and how they can use it\. When you create your customer managed key, you can specify a key policy\. For more information, see [Managing access to KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/control-access-overview.html#managing-access) in the *AWS Key Management Service Developer Guide*\.

Following is an example key policy which gives a user the permissions they need to call all Voice ID APIs using the customer managed key:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Allow key access to Amazon Connect VoiceID.",
            "Effect": "Allow",
            "Principal": {
                "AWS": "your_user_or_role_ARN"
            },
            "Action": [
                "kms:CreateGrant",
                "kms:Decrypt",
                "kms:DescribeKey"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "kms:ViaService": [
                        "voiceid.region.amazonaws.com"
                    ]
                }
            }
        }
    ]
}
```

For information about specifying permissions in a policy, see [Specifying KMS keys in IAM policy statements](https://docs.aws.amazon.com/kms/latest/developerguide/cmks-in-iam-policies.html) in the AWS Key Management Service Developer Guide\. 

For information about troubleshooting key access, see [Troubleshooting key access](https://docs.aws.amazon.com/kms/latest/developerguide/policy-evaluation.html) in the AWS Key Management Service Developer Guide\. 

### Voice ID encryption context<a name="voiceid-encryption-context"></a>

An [encryption context](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#encrypt_context) is an optional set of key\-value pairs that contain additional contextual information about the data\. AWS KMS uses the encryption context as [ additional authenticated data](https://docs.aws.amazon.com/crypto/latest/userguide/cryptography-concepts.html#term-aad) to support [authenticated encryption](https://docs.aws.amazon.com/crypto/latest/userguide/cryptography-concepts.html#define-authenticated-encryption)\. 

When you include an encryption context in a request to encrypt data, AWS KMS binds the encryption context to the encrypted data\. To decrypt data, you include the same encryption context in the request\. 

Voice ID uses the same encryption context in all AWS KMS cryptographic operations, where the key is `aws:voiceid:domain:arn` and the value is the resource Amazon Resource Name \(ARN\) [Amazon Resource Name \(ARN\)](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\.

```
"encryptionContext": {
   "aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId"
}
```

You can also use the encryption context in audit records and logs to identify how the customer managed key is being used\. The encryption context also appears in logs generated by CloudTrail or Amazon CloudWatch Logs\.

#### Using encryption context to control access to your customer managed key<a name="encryption-context-customer-managed-key"></a>

You can use the encryption context in key policies and IAM policies as conditions to control access to your symmetric customer managed key\. You can also use encryption context constraints in a grant\.

Amazon Connect Voice ID uses an encryption context constraint in grants to control access to the customer managed key in your account or Region\. The grant constraint requires that the operations that the grant allows use the specified encryption context\.

The following are example key policy statements to grant access to a customer managed key for a specific encryption context\. The condition in this policy statement requires that the grants have an encryption context constraint that specifies the encryption context\.

```
{
    "Sid": "Enable DescribeKey",
    "Effect": "Allow",
    "Principal": {
        "AWS": "arn:aws:iam::111122223333:role/ExampleReadOnlyRole"
     },
     "Action": "kms:DescribeKey",
     "Resource": "*"
},
{
     "Sid": "Enable CreateGrant",
     "Effect": "Allow",
     "Principal": {
         "AWS": "arn:aws:iam::111122223333:role/ExampleReadOnlyRole"
     },
     "Action": "kms:CreateGrant",
     "Resource": "*",
     "Condition": {
         "StringEquals": {
             "kms:EncryptionContext:"aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId""
          }
     }
}
```

### Monitoring your encryption keys for Voice ID<a name="monitoring-encryption-keys"></a>

When you use an AWS KMS customer managed key with Voice ID, you can use [AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) or [Amazon CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html) to track requests that Voice ID sends to AWS KMS\. 

The following examples is a sample AWS CloudTrail event for `CreateGrant` operation called by Voice ID to access data encrypted by your customer managed key: 

------
#### [ CreateGrant ]

```
{
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "AROA5STZEFPSZEOW7NP3X:SampleUser1",
        "arn": "arn:aws:sts::111122223333:assumed-role/SampleRole/SampleUser",
        "accountId": "111122223333",
        "accessKeyId": "AAAAAAA1111111EXAMPLE",  
        "sessionContext": {
            "sessionIssuer": {
                "type": "Role",
                "principalId": "AROA5STZEFPSZEOW7NP3X",
                "arn": "arn:aws:iam::111122223333:role/SampleRole",
                "accountId": "111122223333",
                "userName": "SampleUser"
            },
            "webIdFederationData": {},
            "attributes": {
                "creationDate": "2021-09-14T23:02:23Z",
                "mfaAuthenticated": "false"
            }
        },
        "invokedBy": "voiceid.amazonaws.com"
    },
    "eventTime": "2021-09-14T23:02:50Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "CreateGrant",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "SampleIpAddress",
    "userAgent": "Example Desktop/1.0 (V1; OS)",
    "requestParameters": {
        "constraints": {
            "encryptionContextSubset": {
                "aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId"
            }
        },
        "retiringPrincipal": "voiceid.amazonaws.com",
        "keyId": "arn:aws:kms:us-west-2:111122223333:key/44444444-3333-2222-1111-EXAMPLE11111",
        "operations": [
            "CreateGrant",
            "Decrypt",
            "DescribeKey",
            "GenerateDataKey",
            "GenerateDataKeyPair",
            "GenerateDataKeyPairWithoutPlaintext",
            "GenerateDataKeyWithoutPlaintext",
            "ReEncryptFrom",
            "ReEncryptTo"
        ],
        "granteePrincipal": "voiceid.amazonaws.com "
    },
    "responseElements": {
        "grantId": "00000000000000000000000000000cce47be074a8c379ed39f22b155c6e86af82"
    },
    "requestID": "ed0fe4ab-305b-4388-8adf-7e8e3a4e80fe",
    "eventID": "31d0d7c6-ce5b-4caf-901f-025bf71241f6",
    "readOnly": false,
    "resources": [
        {
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-west-2:111122223333:key/00000000-1111-2222-3333-9999999999999"
        }
    ],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "eventCategory": "Management"
}
```

------
#### [ DescribeKey ]

```
{
    "eventVersion": "1.08",
    "userIdentity": {
      "type": "AWSService",
      "invokedBy": "voiceid.amazonaws.com"
    },
    "eventTime": "2021-10-13T15:12:39Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "DescribeKey",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "voiceid.amazonaws.com",
    "userAgent": "voiceid.amazonaws.com",
    "requestParameters": {
        "keyId": "alias/sample-key-alias"
    },
    "responseElements": null,
    "requestID": "ed0fe4ab-305b-4388-8adf-7e8e3a4e80fe",
    "eventID": "31d0d7c6-ce5b-4caf-901f-025bf71241f6",
    "readOnly": true,
    "resources": [{
        "accountId": "111122223333",
        "type": "AWS::KMS::Key",
        "ARN": "arn:aws:kms:us-west-2:111122223333:key/00000000-1111-2222-3333-9999999999999"
    }],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "eventCategory": "Management"
}
```

------
#### [ Decrypt ]

```
{
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AWSService",
        "invokedBy": "voiceid.amazonaws.com"
    },
    "eventTime": "2021-10-12T23:59:34Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "Decrypt",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "voiceid.amazonaws.com",
    "userAgent": "voiceid.amazonaws.com",
    "requestParameters": {
        "encryptionContext": {
            "keyId": "arn:aws:kms:us-west-2:111122223333:key/44444444-3333-2222-1111-EXAMPLE11111",
            "encryptionContext": {
                "aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId"
            },
            "encryptionAlgorithm": "SYMMETRIC_DEFAULT"
        },
        "responseElements": null,
        "requestID": "ed0fe4ab-305b-4388-8adf-7e8e3a4e80fe",
        "eventID": "31d0d7c6-ce5b-4caf-901f-025bf71241f6",
        "readOnly": true,
        "resources": [{
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-west-2:111122223333:key/00000000-1111-2222-3333-9999999999999"
        }],
        "eventType": "AwsApiCall",
        "managementEvent": true,
        "recipientAccountId": "111122223333",
        "sharedEventID": "35d58aa1-26b2-427a-908f-025bf71241f6",
        "eventCategory": "Management"
    }
```

------
#### [ GenerateDataKeyWithoutPlaintext ]

```
{
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AWSService",
        "invokedBy": "voiceid.amazonaws.com"
    },
    "eventTime": "2021-10-13T00:26:41Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "GenerateDataKeyWithoutPlaintext",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "voiceid.amazonaws.com",
    "userAgent": "voiceid.amazonaws.com",
    "requestParameters": {
        "keyId": "arn:aws:kms:us-west-2:111122223333:key/44444444-3333-2222-1111-EXAMPLE11111",
        "encryptionContext": {
            "aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId"
        },
        "keySpec": "AES_256"
    },
    "responseElements": null,
    "requestID": "ed0fe4ab-305b-4388-8adf-7e8e3a4e80fe",
    "eventID": "31d0d7c6-ce5b-4caf-901f-025bf71241f6",
    "readOnly": true,
    "resources": [{
        "accountId": "111122223333",
        "type": "AWS::KMS::Key",
        "ARN": "arn:aws:kms:us-west-2:111122223333:key/00000000-1111-2222-3333-9999999999999"
    }],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "sharedEventID": "35d58aa1-26b2-427a-908f-025bf71241f6",
    "eventCategory": "Management"
}
```

------
#### [ ReEncrypt ]

```
{
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AWSService",
        "invokedBy": "voiceid.amazonaws.com"
    },
    "eventTime": "2021-10-13T00:59:05Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "ReEncrypt",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "voiceid.amazonaws.com",
    "userAgent": "voiceid.amazonaws.com",
    "requestParameters": {
        "destinationEncryptionContext": {
            "aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId"
        },
        "destinationKeyId": "arn:aws:kms:us-west-2:111122223333:key/44444444-3333-2222-1111-EXAMPLE11111",
        "sourceEncryptionAlgorithm": "SYMMETRIC_DEFAULT",
        "sourceAAD": "SampleSourceAAAD+JXBmH+ZJNM73BfHE/dwQALXp7Sf44VwvoJOrLj",
        "destinationAAD": "SampleDestinationAAAD+JXBmH+ZJNM73BfHE/dwQALXp7Sf44VwvoJOrLj",
        "sourceEncryptionContext": {
            "aws:voiceid:domain:arn": "arn:aws:voiceid:us-west-2:111122223333:domain/sampleDomainId"
        },
        "destinationEncryptionAlgorithm": "SYMMETRIC_DEFAULT",
        "sourceKeyId": "arn:aws:kms:us-west-2:111122223333:key/55555555-3333-2222-1111-EXAMPLE22222"
    },
    "responseElements": null,
    "requestID": "ed0fe4ab-305b-4388-8adf-7e8e3a4e80fe",
    "eventID": "31d0d7c6-ce5b-4caf-901f-025bf71241f6",
    "readOnly": true,
    "resources": [{
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-west-2:111122223333:key/00000000-1111-2222-3333-9999999999999"
        },
        {
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-west-2:111122223333:key/00000000-1111-2222-3333-7777777777777"
        }
    ],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "sharedEventID": "35d58aa1-26b2-427a-908f-025bf71241f6",
    "eventCategory": "Management"
}
```

------

## High\-Volume Outbound Communications<a name="encryption-at-rest-outboundcommunications"></a>

For Amazon Connect High\-Volume Outbound Communications, Amazon Pinpoint passes customer phone numbers and relevant attributes to Amazon Connect\. On Amazon Connect, these are always encrypted at rest using either a customer managed key or an AWS owned key\. The Amazon Connect High\-Volume Outbound Communications data is segregated by the Amazon Connect instance ID and are encrypted by instance specific keys\.

You can provide your own customer managed key when onboarding to Amazon Connect High\-Volume Outbound Communications\.

The service use this customer managed key to encrypt sensitive data at rest\. The customer managed key is created, owned, and managed by you\. You have full control over the customer managed key 

If you do not provide your own customer managed key, then Amazon Connect High\-Volume Outbound Communications encrypts sensitive data at rest using a AWS owned key specific to your Amazon Connect instance\.

AWS KMS charges apply for a customer managed key\. For more information about pricing, see [AWS KMS pricing](http://aws.amazon.com/kms/pricing/)\. 