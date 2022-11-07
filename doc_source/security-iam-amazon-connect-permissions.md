# Required permissions for using custom IAM policies to manage access to the Amazon Connect console<a name="security-iam-amazon-connect-permissions"></a>

If you're using custom [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) policies to manage access to the Amazon Connect console, your users need some or all of the permissions listed in this article, depending on the tasks they need to do\. 

**Note**  
Using **connect:\*** in a custom IAM policy grants your users all of the Amazon Connect permissions listed in this article\.

**Note**  
Certain pages on the Amazon Connect console, such as [Tasks](#tasks-page) and [Customer Profiles](#customer-profiles-page), require that you add permissions to your inline policies\. 

## AmazonConnect\_FullAccess policy<a name="amazonconnectfullaccesspolicy"></a>

To allow full read/write access to Amazon Connect, you must attach two policies to your IAM users, groups, or roles\. Attach the **AmazonConnect\_FullAccess** policy and a custom policy with the following contents:

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

To allow an IAM user to create an instance, ensure that they have the permissions granted by the AmazonConnect\_FullAccess policy\.

When you use AmazonConnect\_FullAccess policy, note the following:
+ Additional privileges are required to create a Amazon S3 bucket with a name of your choosing, or use an existing bucket while creating or updating an instance from the Amazon Connect console\. If you choose default storage locations for your call recordings, chat transcripts, call transcripts, etc, they are now prefixed with "amazon\-connect\-"\.
+ The aws/connect KMS key is available to use as a default encryption option\. To use a custom encryption key, assign users additional KMS privileges\.
+ Assign users additional privileges to attach other AWS resources like Amazon Polly, Live Media Streaming, Data Streaming, and Lex bots to their Amazon Connect instances\. 

## AmazonConnectReadOnlyAccess policy<a name="amazonconnectreadonlyaccesspolicy"></a>

To allow read\-only access, you need to attach only the **AmazonConnectReadOnlyAccess** policy\.

## Amazon Connect console home page<a name="console-home-page-permissions"></a>

The following image shows a sample Amazon Connect console home page\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/iam-custom-permissions-admin-console-home-page.png)

Use the permissions listed in the following table to manage access to this page\.


| Action/Use case | Permissions needed | 
| --- | --- | 
| List instance  | connect:ListInstances ds:DescribeDirectories  | 
| Describe instance: View the details of the instance/ current settings  | connect:DescribeInstance connect:ListLambdaFunctions connect:ListLexBots connect:ListInstanceStorageConfigs connect:ListApprovedOrigins connect:ListSecurityKeys connect:DescribeInstanceAttributes connect:DescribeInstanceStorageConfig ds:DescribeDirectories  | 
| Create instance  | connect:CreateInstance connect:DescribeInstance connect:ListInstances connect:AssociateInstanceStorageConfig connect:UpdateInstanceAttribute ds:CheckAlias ds:CreateAlias ds:AuthorizeApplication ds:UnauthorizeApplication ds:CreateIdentityPoolDirectory ds:CreateDirectory ds:DescribeDirectories iam:CreateServiceLinkedRole  kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant logs:CreateLogGroup s3:CreateBucket s3:GetBucketLocation s3:ListAllMyBuckets servicequotas:GetServiceQuota  profile:ListAccountIntegrations profile:GetDomain  profile:ListDomains profile:GetProfileObjectType  profile:ListProfileObjectTypeTemplates  | 
| Delete instance  |  connect:DescribeInstance connect:DeleteInstance connect:ListInstances ds:DescribeDirectories ds:DeleteDirectory ds:UnauthorizeApplication  | 

## Detailed instance pages<a name="detail-pages"></a>

The following image shows how you navigate to each of the detailed instance pages:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/iam-custom-permissions-admin-console-telephony-page.png)

To access the detailed instance pages, you need permissions to the Amazon Connect console home page \(describe/list\)\. Or, use the **AmazonConnectReadOnlyAccess** policy\.

The following tables list the granular permissions for each detailed instance page\.

**Note**  
To perform **Edit** actions, users also need **List** and **Describe** permissions\.

### Overview page<a name="overview-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| Create service\-linked role |  connect:DescribeInstance connect:ListInstances connect:DescribeInstanceAttribute connect:UpdateInstanceAttribute connect:ListIntegrationAssociations profile:ListAccountIntegrations ds:DescribeDirectories iam:CreateServiceLinkedRole iam:PutRolePolicy  | 

### Telephony page<a name="telephony-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View telephony options | connect:DescribeInstance | 
| Enable/Disable telephony options   |  connect:UpdateInstanceAttribute  | 
| View outbound campaigns  |  connect\-campaigns:GetConnectInstanceConfig  connect\-campaigns:GetInstanceOnboardingJobStatus connect:DescribeInstance connect:DescribeInstanceAttribute kms:DescribeKey  | 
| Enable/disable outbound campaigns  |  connect\-campaigns:GetConnectInstanceConfig  connect\-campaigns:GetInstanceOnboardingJobStatus connect\-campaigns:StartInstanceOnboardingJob connect\-campaigns:DeleteInstanceOnboardingJob connect\-campaigns:DeleteConnectInstanceConfig connect:DescribeInstance connect:DescribeInstanceAttribute connect:UpdateInstanceAttribute iam:CreateServiceLinkedRole  iam:DeleteServiceLinkedRole  iam:AttachRolePolicy  iam:PutRolePolicy  iam:DeleteRolePolicy  events:PutRule  events:PutTargets  events:DeleteRule  events:RemoveTargets events:DescribeRule events:ListTargetsByRule  ds:DescribeDirectories  kms:DescribeKey kms:ListKeys  kms:CreateGrant  kms:RetireGrant  | 

### Data storage page<a name="data-storage-page"></a>

#### Call recording section<a name="call-recording-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View call recording | connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig | 
| Edit call recording  |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:GetBucketAcl s3:CreateBucket kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant   | 

#### Chat transcripts section<a name="chat-transcripts-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View chat transcripts | connect:DescribeInstance connect:DescribeInstanceStorageConfig connect:ListInstanceStorageConfigs  | 
| Edit chat transcripts |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:GetBucketAcl s3:CreateBucket kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant   | 

#### Attachments section<a name="attachments-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View chat attachments | connect:DescribeInstance connect:DescribeInstanceStorageConfig connect:ListInstanceStorageConfigs  | 
| Edit chat attachments |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:CreateBucket s3:GetBucketAcl kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant   | 

#### Live media streaming section<a name="live-media-streaming-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View live media streaming | connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit live media streaming |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig kms:CreateGrant kms:DescribeKey kms:RetireGrant   | 

#### Exported reports section<a name="exported-reports-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View exported reports | connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit exported reports |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect: DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:CreateBucket kms:DescribeKey kms:ListAliases kms:RetireGrant kms:CreateGrant   | 

### Data streaming page<a name="data-streaming-page"></a>

#### Contact records section<a name="ctr-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View data streaming \- Contact records |  connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit contact record |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig firehose:ListDeliveryStreams firehose:DescribeDeliveryStream kinesis:ListStreams kinesis:DescribeStream   | 

#### Agent events section<a name="agent-events-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View data streaming \- Agent events |  connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit agent events |  connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig kinesis:ListStreams kinesis: DescribeStream   | 

### Application integration page<a name="application-integration-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View approved origins | connect:DescribeInstance connect:ListApprovedOrigins  | 
| Edit approved origins |  connect: AssociateApprovedOrigin connect:ListApprovedOrigins connect:DisassociateApprovedOrigin  | 

### Tasks page<a name="tasks-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Tasks integrations | app\-integrations:GetEventIntegration connect:ListIntegrationAssociations  | 
| Edit Tasks integrations | app\-integrations:CreateEventIntegration app\-integrations:GetEventIntegration app\-integrations:ListEventIntegrations app\-integrations:DeleteEventIntegrationAssociation app\-integrations:CreateEventIntegrationAssociation appflow:CreateFlow appflow:CreateConnectorProfile appflow:DescribeFlow appflow:DeleteFlow appflow:DeleteConnectorProfile appflow:DescribeConnectorEntity appflow:ListFlows appflow:ListConnectorEntities appflow:StartFlow connect:ListIntegrationAssociations connect:DeleteIntegrationAssociation connect:ListUseCases connect:DeleteUseCase events:ActivateEventSource events:CreateEventBus events:DescribeEventBus events:DescribeEventSource events:ListEventSources events:ListTargetsByRule events:PutRule events:PutTargets events:DeleteRule events:RemoveTargets kms:CreateGrant kms:DescribeKey kms:ListAliases kms:ListKeys kms:ListGrants  | 

### Customer profiles page<a name="customer-profiles-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View customer profiles | appflow:DescribeFlow appflow:DescribeConnectorEntity appflow:ListFlows appflow:ListConnectorEntities appflow:ListConnectorProfiles kms:ListKeys profile:ListDomains profile:ListAccountIntegrations sqs:ListQueues  | 
| Edit customer profiles | appflow:CreateFlow appflow:CreateConnectorProfile appflow:DescribeFlow appflow:DeleteFlow appflow:DescribeConnectorEntity appflow:ListFlows appflow:ListConnectorEntities appflow:ListConnectorProfiles appflow:StartFlow appflow:StopFlow kms:ListKeys profile:CreateDomain profile:DeleteIntegration profile:DeleteDomain profile:ListDomains profile:ListAccountIntegrations profile:PutIntegration profile:UpdateDomain kms:ListGrants kms:DescribeKey kms:ListAliases kms:ListKeys sqs:ListQueues  | 

### Voice ID page<a name="voiceid-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Voice ID integrations | voiceid:DescribeDomain voiceid:ListDomains voiceid:RegisterComplianceConsent voiceid:DescribeComplianceConsent connect:ListIntegrationAssociations  | 
| Edit Voice ID integrations | voiceid:DescribeDomain voiceid:ListDomains voiceid:RegisterComplianceConsent voiceid:DescribeComplianceConsent voiceid:UpdateDomain voiceid:CreateDomain connect:ListIntegrationAssociations connect:CreateIntegrationAssociation connect:DeleteIntegrationAssociation events:PutRule events:DeleteRule events:PutTargets events:RemoveTargets  | 

### Flows page<a name="contact-flows-page"></a>

#### Flows security keys section<a name="security-keys-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View flow security keys | connect:DescribeInstance connect:ListSecurityKeys  | 
| Add/remove flow security keys |  connect:AssociateSecurityKey connect:DisassociateSecurityKey  | 

#### Lex bots section<a name="lex-bots-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Lex bots | connect:ListLexBots connect:ListBots  | 
| Add/remove Lex bots |  lex:GetBots lex:GetBot  lex:CreateResourcePolicy lex:DeleteResourcePolicy lex:UpdateResourcePolicy lex:DescribeBotAlias lex:ListBotAliases lex:ListBots connect:AssociateBot connect:DisassociateBot connect:ListBots connect:AssociateLexBot connect:DisassociateLexBot connect:ListLexBots   | 

#### Lambda functions section<a name="lambda-functions-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Lambda functions | connect:ListLambdaFunctions  | 
| Add/remove Lambda functions |  connect:ListLambdaFunctions connect:AssociateLambdaFunction connect:DisassociateLambdaFunction lambda:ListFunctions lambda:AddPermission lambda:RemovePermission  | 

#### Flow logs section<a name="contact-flow-logs-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View flow log config | connect:DescribeInstance connect:DescribeInstanceAttribute  | 
| Enable/disable flow log |  logs:CreateLogGroup   | 

#### Amazon Polly section<a name="amazon-polly-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Amazon Polly option | connect:DescribeInstance connect:DescribeInstanceAttribute  | 
| Update Amazon Polly option |  connect:UpdateInstanceAttribute  | 

## Federations<a name="federations"></a>

### SAML federation<a name="saml-federation"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| SAML federation | connect:GetFederationToken  | 

### Admin/Emergency federation<a name="admin-emergency-federation"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| Admin/Emergency federation | connect:GetFederationTokens  | 