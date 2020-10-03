# Required permissions for managing access to the Amazon Connect console<a name="security-iam-amazon-connect-permissions"></a>

To allow read\-only access, you need to attach only the **AmazonConnectReadOnlyAccess** policy\.

To manage your Amazon Connect instance using the Amazon Connect console, your users need some or all of the permissions listed in this article, depending on the tasks they need to do\.

**Note**  
Using **connect:\*** grants your users all of the Amazon Connect permissions listed in this article\.

## Amazon Connect console home page<a name="console-home-page-permissions"></a>

The following image shows a sample Amazon Connect console home page\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/iam-custom-permissions-admin-console-home-page.png)

Use the permissions listed in the following table to manage access to this page\.


| Action/Use case | Permissions needed | 
| --- | --- | 
| List instance  | connect:ListInstances ds:DescribeDirectories  | 
| Describe instance: View the details of the instance/ current settings  | connect:DescribeInstance connect:GetDataStreamConfig connect:GetMediaStreamingConfig connect:ListLambdaFunctions connect:ListLexBots connect:ListInstanceStorageConfigs connect:ListApprovedOrigins connect:ListSecurityKeys connect:DescribeInstanceAttributes connect:DescribeInstanceStorageConfig ds:DescribeDirectories  | 
| Create instance  | connect:CreateInstance connect:DescribeInstance connect:ListInstances connect:AssociateInstanceStorageConfig connect:UpdateInstanceAttribute ds:CheckAlias ds:CreateAlias ds:AuthorizeApplication ds:UnauthorizeApplication ds:CreateIdentityPoolDirectory ds:CreateDirectory ds:DescribeDirectories iam:CreateServiceLinkedRole iam:AttachRolePolicy iam:PutRolePolicy kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant logs:CreateLogGroup s3:CreateBucket s3:GetBucketLocation s3:ListAllMyBuckets servicequotas:GetServiceQuota  | 
| Delete instance  |  connect:DestroyInstance connect:DescribeInstance connect:DeleteInstance connect:ListInstances ds:DescribeDirectories ds:DeleteDirectory ds:UnauthorizeApplication  | 

## Detailed instance pages<a name="detail-pages"></a>

The following image shows how you navigate to each of the detailed instance pages:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/iam-custom-permissions-admin-console-telephony-page.png)

To access the detailed instance pages, you need permissions to the Amazon Connect console home page \(describe/list\)\. Or, use the **AmazonConnectReadOnlyAccess** policy\.

The following tables list the granular permissions for each detailed instance page\.

**Note**  
To perform **Edit** actions, users also need **List** and **Describe** permissions\.

### Overview and Telephony options pages<a name="telephony-options-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View telephony options | connect:DescribeInstance | 
| Enable/Disable telephony options   | connect:ModifyInstance connect:UpdateInstanceAttribute  | 

### Data storage page<a name="data-storage-page"></a>

#### Call recording section<a name="call-recording-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View call recording | connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig | 
| Edit call recording  | connect:ModifyInstance connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:GetBucketAcl s3:CreateBucket kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant iam:PutRolePolicy iam:AttachRolePolicy  | 

#### Chat transcripts section<a name="chat-transcripts-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View chat transcripts | connect:DescribeInstance connect:DescribeInstanceStorageConfig connect:ListInstanceStorageConfigs  | 
| Edit chat transcripts | connect:DescribeInstance connect:AssociateInstanceStorage connect:DisassociateInstanceStorage connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:CreateBucket kms:CreateGrant kms:DescribeKey kms:ListAliases kms:RetireGrant iam:PutRolePolicy iam:AttachRolePolicy  | 

#### Live media streaming section<a name="live-media-streaming-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View live media streaming | connect:DescribeInstance connect:GetMediaStreamingConfig connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit live media streaming |  connect:UpdateMediaStreamingConfig connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig kms:CreateGrant kms:DescribeKey kms:RetireGrant iam:PutRolePolicy iam:AttachRolePolicy  | 

#### Exported reports section<a name="exported-reports-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View exported reports | connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit exported reports | connect:ModifyInstance connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect: DisassociateInstanceStorageConfig s3:ListAllMyBuckets s3:GetBucketLocation s3:CreateBucket kms:DescribeKey kms:ListAliases kms:RetireGrant kms:CreateGrant iam:PutRolePolicy iam:AttachRolePolicy  | 

### Data streaming page<a name="data-streaming-page"></a>

#### Contact trace records section<a name="ctr-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View data streaming \- Contact trace records | connect:GetDataStreamConfig connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit contact trace record | connect:UpdateDataStreamConfig connect:ModifyInstance connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig connect:DescribeInstance firehose:ListDeliveryStreams firehose:DescribeDeliveryStream kinesis:ListStreams kinesis:DescribeStream iam:PutRolePolicy iam:AttachRolePolicy  | 

#### Agent events section<a name="agent-events-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View data streaming \- Agent events | connect:GetDataStreamConfig connect:DescribeInstance connect:ListInstanceStorageConfigs connect:DescribeInstanceStorageConfig  | 
| Edit agent events | connect:UpdateDataStreamConfig connect:DescribeInstance connect:AssociateInstanceStorageConfig connect:UpdateInstanceStorageConfig connect:DisassociateInstanceStorageConfig kinesis:ListStreams kinesis: DescribeStream iam:PutRolePolicy iam:AttachRolePolicy  | 

### Application integration page<a name="application-integration-page"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View approved origins | connect:DescribeInstance connect:ListApprovedOrigins  | 
| Edit approved origins | connect:ModifyInstance connect: AssociateApprovedOrigin connect:ListApprovedOrigins connect:DisassociateApprovedOrigin  | 

### Contact flows page<a name="contact-flows-page"></a>

#### Contact flows security keys section<a name="security-keys-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View contact flow security keys | connect:DescribeInstance connect:ListSecurityKeys  | 
| Add/remove contact flow security keys | connect:ModifyInstance connect:AssociateSecurityKey connect:DisassociateSecurityKey  | 

#### Lex bots section<a name="lex-bots-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Lex bots | connect:ListLexBots  | 
| Add/remove Lex bots | connect:DescribeInstance lex:GetBots lex:GetBot connect:AddLexBots connect:RemoveLexBots connect:AssociateLexBot connect:DisassociateLexBot connect:ListLexBots iam:PutRolePolicy iam:AttachRolePolicy  | 

#### Lambda functions section<a name="lambda-functions-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View Lambda functions | connect:ListLambdaFunctions  | 
| Add/remove Lambda functions | connect:RemoveLambdaFunctions connect:AddLambdaFunctions connect:ListLambdaFunctions connect:AssociateLambdaFunction connect:DisassociateLambdaFunction lambda:ListFunctions lambda:AddPermission lambda:RemovePermission  | 

#### Contact flow logs section<a name="contact-flow-logs-section"></a>


| Action/Use case | Permissions needed | 
| --- | --- | 
| View contact flow log config | connect:DescribeInstance connect:DescribeInstanceAttribute  | 
| Enable/disable contact flow log | connect:ModifyInstance logs:CreateLogGroup   | 

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