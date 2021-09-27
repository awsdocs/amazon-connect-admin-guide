# Logging Amazon Connect API calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

Amazon Connect is integrated with AWS CloudTrail, a service that provides a record of the Amazon Connect API calls that a user, role, or AWS service makes\. CloudTrail captures Amazon Connect API calls as events\. All public Amazon Connect APIs support CloudTrail\. 

**Note**  
Events from the Amazon Connect admin console aren't recorded in CloudTrail\. If you have a custom integration that uses the Amazon Connect API, those events will be logged\.

Using the information that CloudTrail collects, you can identify a specific request to an Amazon Connect API, the IP address of the requester, the requester's identity, the date and time of the request, and so on\. If you configure a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket\. If you don't configure a trail, you can view the most recent events in **Event History** in the CloudTrail console\.

For more information about CloudTrail, including how to configure and enable it, see [Creating a Trail For Your AWS Account](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html) and [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)\.

## Amazon Connect information in CloudTrail<a name="connect-info-in-cloudtrail"></a>

CloudTrail is enabled on your AWS account when you create the account\. When supported event activity occurs in Amazon Connect, that activity is recorded in a CloudTrail event along with other AWS service events in **Event history**\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing Events with CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\. 

For an ongoing record of events in your AWS account, including events for Amazon Connect, create a trail\. A *trail* enables CloudTrail to deliver log files to an Amazon S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all AWS Regions and delivers the log files to the Amazon S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs\. For more information, see the following: 
+ [Creating a Trail For Your AWS Account](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html#cloudtrail-aws-service-specific-topics-integrations)
+ [Configuring Amazon SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)
+ [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

Every event or log entry contains information about who generated the request\. The identity information helps you determine the following: 
+ Whether the request was made with root or AWS Identity and Access Management \(IAM\) user credentials\.
+ Whether the request was made with temporary security credentials for a role or federated user\.
+ Whether the request was made by another AWS service\.

For more information, see the [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

## Example: Amazon Connect log file entries<a name="understanding-connect-entries"></a>

 A trail is a configuration that enables delivery of events as log files to an Amazon S3 bucket that you specify\. CloudTrail log files contain one or more log entries\. An event represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. CloudTrail log files aren't an ordered stack trace of the public API calls, so they don't appear in any specific order\.

The following example shows a CloudTrail log entry that demonstrates the `GetContactAttributes` action\.

```
{
        "eventVersion": "1.05",
        "userIdentity": {
         "type": "AssumedRole",
         "principalId": "AAAAAAA1111111EXAMPLE",
         "arn": "arn:aws:sts::123456789012:assumed-role/John",
         "accountId": "123456789012",
         "accessKeyId": "AAAAAAA1111111EXAMPLE",          
         "sessionContext": {
            "attributes": {
                "mfaAuthenticated": "false",
                "creationDate": "2019-08-15T06:40:14Z"
            },
            "sessionIssuer": {
                "type": "Role",
                "principalId": "AAAAAAA1111111EXAMPLE",
                "arn": "arn:aws:iam::123456789012:role/John",
                "accountId": "123456789012",
                "userName": "John"
            }
        }
    },
    "eventTime": "2019-08-15T06:40:55Z",
    "eventSource": "connect.amazonaws.com",
    "eventName": "GetContactAttributes",
    "awsRegion": "us-west-2",
    "sourceIPAddress": "205.251.233.179",
    "userAgent": "aws-sdk-java/1.11.590 Mac_OS_X/10.14.6 Java_HotSpot(TM)_64-Bit_Server_VM/25.202-b08 java/1.8.0_202 vendor/Oracle_Corporation",
    "requestParameters": {
        "InitialContactId": "00fbeee1-123e-111e-93e3-11111bfbfcc1",
        "InstanceId": "00fbeee1-123e-111e-93e3-11111bfbfcc1"
    },
    "responseElements": null,
    "requestID": "be1bee1d-1111-11e1-1eD1-0dc1111f1ac1c",
    "eventID": "00fbeee1-123e-111e-93e3-11111bfbfcc1",
    "readOnly": true,
    "eventType": "AwsApiCall",
    "recipientAccountId": "123456789012"
}
```

## Example: Amazon Connect Voice ID log file entries<a name="understanding-voiceid-entries"></a>

Just like Amazon Connect, Voice ID is integrated with CloudTrail\. When enabled, the service emits events for the Voice ID API calls made by a user, role, or an AWS service\. You can reuse the same CloudTrail resources created for Amazon Connect, including the trail and the S3 bucket, to receive CloudTrail logs for Voice ID as well\. 

For security reasons, the sensitive fields which might contain PII information in the API requests and responses are redacted in the events\.

The following example shows a CloudTrail log entry that demonstrates the ` CreateDomain` action\.

```
{
  "eventVersion": "1.08",
  "userIdentity": {
    "type": "AssumedRole",
    "principalId": "AROA5STZEFPSWCM4YHJB2:SampleUser",
    "arn": "arn:aws:sts::111122223333:assumed-role/SampleRole/SampleUser",
    "accountId": "111122223333",
    "accessKeyId": "AAAAAAA1111111EXAMPLE",  
    "sessionContext": {
      "sessionIssuer": {
        "type": "Role",
        "principalId": "EXAMPLEZEFPSWCM4YHJB2",
        "arn": "arn:aws:iam::111122223333:role/SampleRole",
        "accountId": "111122223333",
        "userName": "SampleRole"
      },
      "webIdFederationData": {},
      "attributes": {
        "mfaAuthenticated": "false",
        "creationDate": "2021-08-17T01:55:39Z"
      }
    }
  },
  "eventTime": "2021-08-17T01:55:41Z",
  "eventSource": "voiceid.amazonaws.com",
  "eventName": "CreateDomain",
  "awsRegion": "us-west-2",
  "sourceIPAddress": "205.251.233.179",
  "userAgent": "aws-sdk-java/1.11.590 Mac_OS_X/10.14.6 Java_HotSpot(TM)_64-Bit_Server_VM/25.202-b08 java/1.8.0_202 vendor/Oracle_Corporation",
  "requestParameters": {
    "description": "HIDDEN_DUE_TO_SECURITY_REASONS",
    "name": "HIDDEN_DUE_TO_SECURITY_REASONS",
    "serverSideEncryptionConfiguration": {
      "kmsKeyId": "alias/sample-customer-managed-key"
    }
  },
  "responseElements": {
    "domain": {
      "arn": "arn:aws:voiceid:us-west-2:111122223333:domain/ExampleOsAjzg9xoByUatN",
      "createdAt": "Aug 17, 2021, 1:55:40 AM",
      "description": "HIDDEN_DUE_TO_SECURITY_REASONS",
      "domainId": "UcUuCPFOsAjzg9xoByUatN",
      "domainStatus": "ACTIVE",
      "name": "HIDDEN_DUE_TO_SECURITY_REASONS",
      "serverSideEncryptionConfiguration": {
        "kmsKeyId": "arn:aws:kms:us-west-2:111122223333:key/1111111-7741-44b1-a5fe-7c6208589bf3"
      },
      "updatedAt": "Aug 17, 2021, 1:55:40 AM"
    }
  },
  "requestID": "11111111-b358-4637-906e-67437274fe4e",
  "eventID": "1111111-a4d1-445e-ab62-8626af3c458d",
  "readOnly": false,
  "eventType": "AwsApiCall",
  "managementEvent": true,
  "eventCategory": "Management",
  "recipientAccountId": "111122223333"
}
```