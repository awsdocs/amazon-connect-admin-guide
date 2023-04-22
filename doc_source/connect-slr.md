# Use service\-linked roles for Amazon Connect<a name="connect-slr"></a>

## What are service\-linked roles \(SLR\) and why are they important?<a name="what-is-slr"></a>

Amazon Connect uses AWS Identity and Access Management \(IAM\) [service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to an Amazon Connect instance\. 

Service\-linked roles are predefined by Amazon Connect and include [all the permissions](#slr-permissions) that Amazon Connect requires to call other AWS services on your behalf\.

You need to enable service\-linked roles so you can use new features in Amazon Connect, such as tagging support, the new user interface in **User management** and **Routing profiles**, and queues with CloudTrail support\.

For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes** in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for Amazon Connect<a name="slr-permissions"></a>

Amazon Connect uses the service\-linked role with the prefix **AWSServiceRoleForAmazonConnect**\_*unique\-id* – Grants Amazon Connect permission to access AWS resources on your behalf\.

The AWSServiceRoleForAmazonConnect prefixed service\-linked role trusts the following services to assume the role:
+ `connect.amazonaws.com`

The role permissions policy allows Amazon Connect to complete the following actions on the specified resources\. As you enable additional features in Amazon Connect, additional permissions are added for the service\-linked role to access the resources associated with those features:
+ Action: all Amazon Connect actions, `connect:*`, on all Amazon Connect resources\.
+ Action: Amazon S3 `s3:GetObject`, `s3:GetObjectAcl`, `s3:PutObject`, `s3:PutObjectAcl`, `s3:DeleteObject`, `s3:GetBucketLocation`, and `GetBucketAcl` for the S3 bucket specified for recorded conversations\.

  It also grants `s3:PutObject`, `s3:PutObjectAcl`, and `s3:GetObjectAcl` to the bucket specified for exported reports\.
+ Action: Amazon Connect Customer Profiles 
  + `profile:SearchProfiles`
  + `profile:CreateProfile`
  + `profile:UpdateProfile`
  + `profile:AddProfileKey`
  + `profile:ListProfileObjects`
  + `profile:ListAccountIntegrations` 
  + `profile:ListProfileObjectTypeTemplates`
  + `profile:GetProfileObjectTypeTemplate`
  + `profile:ListProfileObjectTypes`
  + `profile:GetProfileObjectType`

  to use your default Customer Profiles domain \(including profiles and all object\-types in domain\) with the Amazon Connect flows and agent experience applications\.
+ Action: Amazon Kinesis Data Firehose `firehose:DescribeDeliveryStream` and `firehose:PutRecord`, and `firehose:PutRecordBatch` for the delivery stream defined for agent event streams and contact records\.
+ Action: Amazon Kinesis Data Streams `kinesis:PutRecord`, `kinesis:PutRecords`, and `kinesis:DescribeStream` for the stream specified for agent event streams and contact records\.
+ Action: Amazon Lex `lex:PostContent` for the bots added to your instance\.
+ Action: Amazon Lex `lex:ListBots`, `lex:ListBotAliases` for all bots created in the account across all Regions\.
+ Action: Amazon CloudWatch Logs `logs:CreateLogStream`, `logs:DescribeLogStreams`, and `logs:PutLogEvents` to the CloudWatch Logs group specified for flow logging\.
+ Action: Amazon CloudWatch Metrics `cloudwatch:PutMetricData` to publish Amazon Connect usage metrics for an instance to your account\.
+ Action: Amazon Connect Voice\-ID `voiceid:*` for the Voice ID domains associated with your instance\.
+ Action: EventBridge `events:PutRule` and `events:PutTargets` for the Amazon Connect managed EventBridge rule for publishing CTR records for your associated Voice ID domains\.
+ Action: outbound campaigns
  + `connect-campaigns:CreateCampaign`
  + `connect-campaigns:DeleteCampaign`
  +  `connect-campaigns:DescribeCampaign`
  + `connect-campaigns:UpdateCampaignName`
  + `connect-campaigns:GetCampaignState`
  +  `connect-campaigns:GetCampaignStateBatch`
  + `connect-campaigns:ListCampaigns`
  + `connect-campaigns:UpdateOutboundCallConfig`
  +  `connect-campaigns:UpdateDialerConfig`
  +  `connect-campaigns:PauseCampaign`
  + `connect-campaigns:ResumeCampaign`
  + `connect-campaigns:StopCampaign` for all operations related to outbound campaigns\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-linked role permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Create a service\-linked role for Amazon Connect<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you create a new instance in Amazon Connect in the AWS Management Console, Amazon Connect creates the service\-linked role for you\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create a new instance in Amazon Connect, Amazon Connect creates the service\-linked role for you again\. 

You can also use the IAM console to create a service\-linked role with the **Amazon Connect \- Full access** use case\. In the IAM CLI or the IAM API, create a service\-linked role with the `connect.amazonaws.com` service name\. For more information, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\. If you delete this service\-linked role, you can use this same process to create the role again\.

## For instances created before October 2018<a name="migrate-slr"></a>

If your Amazon Connect instance was created before October 2018, you don't have service\-linked roles set up\. To create a service\-linked role, on the **Account overview** page, choose **Create service\-linked role**, as shown in the following image\.

![\[The account overview page, the create service-linked role button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/slr-create-slr.png)

For a list of the IAM permissions required to create the service\-linked role, see [Overview page](security-iam-amazon-connect-permissions.md#overview-page) in the [Required permissions for using custom IAM policies to manage access to the Amazon Connect console](security-iam-amazon-connect-permissions.md) topic\.

## Edit a service\-linked role for Amazon Connect<a name="edit-slr"></a>

Amazon Connect does not allow you to edit the AWSServiceRoleForAmazonConnect prefixed service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Checking a service\-linked role has permissions for Amazon Lex<a name="check-slr"></a>

1. On the navigation pane of the IAM console, choose **Roles**\.

1. Choose the name of the role to modify\.

## Delete a service\-linked role for Amazon Connect<a name="delete-slr"></a>

You don't need to manually delete the AWSServiceRoleForAmazonConnect prefixed role\. When you delete your Amazon Connect instance in the AWS Management Console,  Amazon Connect cleans up the resources and deletes the service\-linked role for you\.

## Supported Regions for Amazon Connect service\-linked roles<a name="slr-regions"></a>

Amazon Connect supports using service\-linked roles in all of the regions where the service is available\. For more information, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#connect_region)\.