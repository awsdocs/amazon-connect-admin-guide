# Amazon Connect service quotas<a name="amazon-connect-service-limits"></a>

Your AWS account has default quotas, formerly referred to as limits, for each AWS service\. All service quotas for Amazon Connect can be adjusted unless otherwise noted\.

To request a quota increase, see [Requesting a quota increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) in the *Service Quotas User Guide*\. If the quota is not yet available in Service Quotas, use the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.

**Considerations**
+ You must create your instance because you can submit a service quota increase\.
+ It can take up to a few weeks to increase your service quota\. If you're increasing your quotas as part of a larger project, be sure to add this time to your plan\.
+ Use the same form to submit a request to port your US phone number from your current carrier to Amazon Connect\. For more information about porting phone numbers, see [Port your current phone number](port-phone-number.md)\.
+ This documentation describes the default quotas for new accounts as of October 2020\. Because the quotas have been adjusted over time, the default values for your account might be different than the default values described here\.

## Amazon Connect quotas<a name="connect-quotas"></a>


| Name | Default | Adjustable | 
| --- | --- | --- | 
|  AWS Lambda functions per instance  |  35  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-E3D2F503) | 
|  Agent status per instance  |  50  | No | 
|  Amazon Connect instances per account  |  2  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-AA17A6B9) | 
|  Amazon Lex bots per instance  |  50  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-B93A6612) | 
|  Amazon Lex V2 bot aliases per instance  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-CCEA7427) | 
|  Concurrent active calls per instance   |  10 For more information, see [How contacts are counted](#contact-counting-criteria)\.  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-12AB7C57) | 
|  Concurrent active chats per instance  |  100 This includes chats that are waiting\. If this quota is exceeded, the API call fails with a quota exceeded error\. By default [Maximum contacts in queue](set-maximum-queue-limit.md) is set to your **Concurrent calls per instance** quota\. If you plan to have more chats than that in a queue, submit a request to increase the **Active chats per instance** quota, and then increase the [Maximum contacts in queue](set-maximum-queue-limit.md) setting\.   | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-D4BA6F6E) | 
|  Concurrent active tasks per instance  |  2500 concurrent active tasks All tasks that have not yet ended are considered active and are counted as concurrent tasks: tasks that are being routed in flows, waiting in a queue for an agent, being handled by agents, or being run in After Contact Work \(ACW\)\. By default [Maximum contacts in queue](set-maximum-queue-limit.md) is set to your **Concurrent calls per instance** quota\. If you plan to have more tasks than that in a queue, submit a request to increase the **Active tasks per instance** quota, and then increase the [Maximum contacts in queue](set-maximum-queue-limit.md) setting\.   | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-60553137) | 
|  Contact flows per instance  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-22922690) | 
|  Hours of operation per instance  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-20CD02F7) | 
|  Maximum duration that a task can be scheduled in future  |  6 days  | No | 
|  Modules per instance  |  200  | No | 
|  Phone numbers per instance  |  5  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-8F812903) | 
|  Prompts per instance  |  500  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-0865B754) | 
|  Queues per instance  |  50  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-19A87C94) | 
|  Queues per routing profile per instance  |  50 This quota refers to number of queue/channel combinations per routing profile\. For example, in the following image there are two queues, but there are three queue\-channel combinations: Escalation queue Voice, Escalation queue Chat, and BasicQueue Voice\. This counts three towards the service limit of 50\. ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-queue-channel-combinations.png)  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-516BC0EB) | 
|  Quick connects per instance  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-68BBE2E8) | 
|  Rate of API requests  |  See [Amazon Connect API throttling quotas](#connect-api-quotas)\.  | Yes | 
|  Reports per instance  |  2000 Personal saved reports count towards the reports per instance\. For example, if one of your supervisors saves a report every day, it will count towards your overall number of saved reports per instance\. As a best practice, we recommend you implement policies so reports don't pile up\.   | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-79564E52) | 
|  Routing profiles per instance  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-D3E7BE26) | 
|  Scheduled reports per instance  |  50  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-986AE5E3) | 
|  Security profiles per instance  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-F325A715) | 
|  User hierarchy groups per instance  |  500 This quota applies to the total number of hierarchy groups you have, across all levels\. There is no feature limit for how many hierarchy groups you can have for each level\. For example, one level could have 500 hierarchy groups, which would reach the quota for your instance\.  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-D68AAAE4) | 
|  Users per instance  |  500  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-9A46857E) | 

## Amazon Connect Customer Profiles service quotas<a name="customer-profiles-quotas"></a>


| Name | Default | Adjustable | 
| --- | --- | --- | 
|  Amazon Connect Customer Profiles domains count  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-6603B252) | 
|  Keys per object type  |  10  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-E3D2F503) | 
|  Maximum expiration in days  |  1,096 \(3 years\) This is the expiration of objects and profiles\.  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-3217D1F1) | 
|  Maximum number of integrations  |  50  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-4A5ECB8E) | 
|  Maximum size of all objects for a profile  |  50MB  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-63975AF3) | 
|  Object and profile maximum size  |  250KB  | No | 
|  Object types per domain  |  100  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-14092FF4) | 
|  Objects per profile  |  1000 This is the maximum number of objects that can be attached to a profile\.  | [Yes](https://console.aws.amazon.com/servicequotas/home/services/connect/quotas/L-E17DC7C3) | 
|  Maximum number of Identity Resolution Jobs each week for a domain  |  3  | No | 
|  Maximum number of consolidation rules in an Identity Resolution Job  |  10  | No | 
|  Maximum number of attributes in each consolidation rule  |  20  | No | 

## Amazon Connect Voice ID service quotas<a name="voiceid-quotas"></a>


| Item | Default quotas  | 
| --- | --- | 
|  Domains  |  3 This quota applies per account\.  | 
|  Concurrent active sessions per domain  |  50 See the following table for information about how to derive your **Concurrent active sessions** quota based on your Amazon Connect call volume\.  | 
|  Maximum number of fraudsters per domain  |  500  | 
|  Maximum number of speakers per domain  |  100,000  | 
|  Active Batch Speaker Enrollment Jobs per domain  |  1  | 
|  Active Batch Fraudster Registration Jobs per domain  |  1  | 
|  Speakers per Batch Speaker Enrollment Job  |  10,000  | 
|  Fraudsters per Batch Fraudster Registration Job  |  500  | 

### Derive Concurrent active sessions based on your Amazon Connect call volume<a name="voiceid-concurrent-active-sessions"></a>

Use the information in the following table to derive your quota for Voice ID **Concurrent active sessions per domain**\. Base your quota on the number of voice calls handled by your Amazon Connect contact center where Voice ID is enabled\.


| Amazon Connect Voice Contacts \(Calls\)/Hour\* | Voice ID Concurrent active sessions | 
| --- | --- | 
|  1,000  |  50  | 
|  5,000  |  250  | 
|  10,000  |  500  | 
|  20,000  |  1,000  | 
|  50,000  |  2,500  | 

\*For the calculations in the preceding table, we assume a fairly uniform distribution of calls during the hour\. If you have more complex traffic patterns, [contact AWS Support](https://console.aws.amazon.com/support/home) with details about your anticipated traffic pattern\.

## Amazon Connect Wisdom service quotas<a name="wisdom-quotas"></a>


| Item | Default quotas  | 
| --- | --- | 
|  Assistants  |  5  | 
|  Knowledge bases  |  10  | 
|  Maximum size of a knowledge base  |  5GB per knowledge base  | 
|  Content per knowledge base  |  10,000  | 
|  Maximum size per document  |  1MB  | 
|  RateLimit for all APIs  |  50TPS  | 

## Feature specifications<a name="feature-limits"></a>

The following table lists feature specifications\.

**Note**  
Feature specifications cannot be increased\.


| Item | Feature Specification | 
| --- | --- | 
| File types supported for chat attachments |  \.csv, \.doc, \.docx, \.jpeg, \.jpg, \.pdf, \.png, \.ppt, \.pptx, \.txt, \.wav, \.xls, \.xlsx   | 
| Max file size for a chat attachment |  20MB  | 
| Attachments per chat conversation |  5  | 
| People who can listen in on the same agent call at the same time  |  5 For example, you can have a group of 5 people listen in to a call at the same time, and then a different group of 5 people listen in to a different call at the same time, and so on\.   | 
| Quick connects you can assign to a queue |  700  | 
| Participants on a conference call |  3 The three participants are the customer, agent, and a third person who can be either another agent or an external third\-party\.  | 
|  Contact record retention  |  24 months from the time the associated contact was initiated\.  You can choose to stream contact records to Kinesis so you can manage retention and perform advanced analysis\.  | 
|  Max size of the contact record attributes section  |  32KB   | 
|  Active chats per agent  |  10  | 
|  Total duration per chat  |  Up to 7 days, including wait time [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-service-limits.html)  | 
|  Characters per chat message  |  1024  | 
|  Open websocket connections per chat participant  |  5  | 
|  Chat Amazon Lex bot integration timeout  |  6 seconds The maximum time within which the Amazon Lex bot must respond to the chat customer's prompt\.  | 
|  Maximum duration of a task  |  7 days  | 
|  Maximum number of transfers for a task  |  11 transfers  | 
|  Maximum number of linked tasks on an existing contact  |  11  | 
|  Limit on creating and deleting instances  | 100 instances can be created or deleted in 30 days Amazon Connect enforces a limit on the **total** number of instances that you can create and delete in 30 days\. If you exceed this limit, you will get an error message indicating there has been an excessive number of attempts at creating or deleting instances\. You must wait 30 days before you can restart creating and deleting instances in your account\. For example, if you create 80 instances and delete 20 over the course of 30 days, you must wait an additional 30 days before you can create or delete any more instances\. If you create and delete the same instance 100 times in 30 days, the limit also applies\.   | 

## Amazon Connect Rules feature specifications<a name="rules-feature-specs"></a>

The following table lists feature specifications\.

**Note**  
Feature specifications cannot be increased\.


| Item | Feature Specification | 
| --- | --- | 
| Published rules per instance |  200  | 
| Draft rules per instance |  50  | 
| Conditions in a rule |  20  | 


| Condition type | Number of entries or selections | Post\-call | Real\-time | 
| --- | --- | --- | --- | 
| Words or phrases \- Exact match |  100  |  Yes  |  Yes  | 
| Words or phrases \- Semantic match |  4  |  Yes  |  Not supported  | 
| Words or phrases \- Pattern match |  100  |  Yes  |  Yes  | 
| Queue condition |  100  |  Yes  |  Yes  | 
| Agent condition |  100  |  Yes  |  Yes  | 
| Custom attributes |  5  |  Yes  |  Yes  | 
| Sentiment \- Time period |  5  |  Yes  |  Yes  | 
| Sentiment \- Entire contact |  5  |  Yes  |  Not supported  | 
| Interruptions |  5  |  Yes  |  Not supported  | 
| Non\-talk time |  5  |  Yes  |  Not supported  | 

## How contacts are counted<a name="contact-counting-criteria"></a>

The following contacts are counted:
+ Handled by a contact flow
+ Waiting in queue
+ Handled by an agent
+ Outbound call

The following contacts are not counted:
+ Callbacks waiting in a callback queue are not counted until the callback is offered to an available agent\.
+ External transfers

If the quota for concurrent active calls per instance is exceeded, contacts get a reorder tone \(also known as a fast busy tone\), which indicates that there is no available transmission path to the called number\.

You can calculate your configured quota using CloudWatch metrics\. For instructions, see [Use CloudWatch metrics to calculate concurrent call quota](monitoring-cloudwatch.md#connect-cloudwatch-concurrent-call-quota)\. 

If you're only taking calls you can also determine your concurrent calls quota by editing a queue and entering an exceptionally large number for the contact limit\. The resulting error message displays your quota for concurrent calls\. For example, in the following image, it shows the call quota for that instance is 9\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/concurrent-call-quota.png)

## Countries you can call<a name="country-code-allow-list"></a>

The Region where your instance is created determines which countries you can call by default\.

 [Submit a service quota increase request](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect) to allow calling to additional countries, or to limit the countries that you can call from\. You must be signed in to your AWS account to access the form\.

For a list of all the countries available for outbound calling, see [Amazon Connect pricing](http://aws.amazon.com/connect/pricing/)\. 

If you already have an instance, the countries that you are allowed to call may be different that those listed in the following sections because we have changed the service quotas over time\.

### Instances created in US East, US West, Canada \(Central\) and AWS GovCloud \(US\-West\)<a name="country-allow-list-us-canada-govcloud"></a>

You can call the following countries by default:
+ United States
+ Canada
+ Mexico
+ Puerto Rico
+ United Kingdom: See [Prefixes that are not allowed by default](#prefixes-not-allowed)

### Instances created in EU \(Frankfurt\) and EU \(London\)<a name="country-allow-list-eu"></a>

You can call the following countries by default:
+ United Kingdom: See [Prefixes that are not allowed by default](#prefixes-not-allowed)
+ Italy
+ France
+ Ireland
+ United States

### Instances created in Asia Pacific \(Tokyo\)<a name="country-allow-list-nrt"></a>

You can call the following countries by default:
+ Japan: See [Prefixes that are not allowed by default](#prefixes-not-allowed)
+ Vietnam
+ United States

### Instances created in Asia Pacific \(Singapore\)<a name="country-allow-list-sin"></a>

You can call the following countries by default:
+ Singapore
+ Australia
+ Hong Kong
+ United States
+ United Kingdom: See [Prefixes that are not allowed by default](#prefixes-not-allowed)

### Instances created in Asia Pacific \(Sydney\)<a name="country-allow-list-syd"></a>

You can call the following countries by default:
+ Australia
+ New Zealand
+ Philippines
+ United States

### Prefixes that are not allowed by default<a name="prefixes-not-allowed"></a>

**UK** numbers with the following prefixes are not allowed by default:
+ \+447 \+44111 \+44118 \+44119 \+448 \+44826 \+449 

Before you can dial these UK mobile numbers, you must submit a service quota increase request\.

**Japan** mobile numbers with the following prefixes are not allowed by default:
+ \+8170, 8180, and 8190

Before you can dial these Japan mobile numbers, you must submit a service quota increase request\.

## Amazon Connect API throttling quotas<a name="connect-api-quotas"></a>

Amazon Connect throttling quotas are by account, and per Region, not by user and not by instance\. For example: 
+ If different IAM users from the same account make requests, they are sharing a throttle bucket\. 
+ If multiple requests are sent from different instances from the same account, they are also sharing a throttle bucket\. 

 When you use the [Amazon Connect Service API ](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html), the number of requests per second is limited to the following:
+ For the [GetMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricData.html) and [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) operations, a RateLimit of 5 requests per second, and a BurstLimit of 8 requests per second\.
**Note**  
The rate limit cannot be increased for GetMetricData and GetCurrentMetricData\.
+ For [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html), [StartContactStreaming](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartContactStreaming.html), [StopContactStreaming](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContactStreaming.html), a RateLimit of 5 requests per second, and a BurstLimit of 8 requests per second\.
+ For all other operations, a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.

## Amazon Connect Participant Service API throttling quotas<a name="connect-participant-api-quotas"></a>

For the Amazon Connect Participant Service, the quotas are by instance\.

 When you use the [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html), the number of requests per second is limited to the following:
+  [CreateParticipantConnection](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateParticipantConnection.html): a RateLimit of 6 requests per second, and a BurstLimit of 9 requests per second\.
+  [DisconnectParticipant](https://docs.aws.amazon.com/connect/latest/APIReference/API_DisconnectParticipant.html): a RateLimit of 3 requests per second, and a BurstLimit of 5 requests per second\.
+  [GetTranscript](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetTranscript.html): a RateLimit of 8 requests per second, and a BurstLimit of 12 requests per second\.
+  [SendEvent](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendEvent.html) and [SendMessage](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendMessage.html): a RateLimit of 10 requests per second, and a BurstLimit of 15 requests per second\.
+  [StartAttachmentUpload](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartAttachmentUpload.html): a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.
+  [CompleteAttachmentUpload](https://docs.aws.amazon.com/connect/latest/APIReference/API_CompleteAttachmentUpload.html): a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.
+  [GetAttachment](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetAttachment.html): a RateLimit of 8 requests per second, and a BurstLimit of 12 requests per second\.

## Amazon Connect Contact Lens Service API throttling quotas<a name="connect-contactlens-api-quotas"></a>

Amazon Connect Contact Lens throttling quotas are by account, not by user and not by instance\. For example:
+ If different IAM users from the same account make requests, they are sharing a throttle bucket\.
+ If multiple requests are sent from different instances from the same account, they are also sharing a throttle bucket\. 

When you use the [Amazon Connect Contact Lens API](https://docs.aws.amazon.com/contact-lens/latest/APIReference/Welcome.html), the number of requests per second is limited to the following:
+ [ListRealtimeContactAnalysisSegments](https://docs.aws.amazon.com/contact-lens/latest/APIReference/ListRealtimeContactAnalysisSegments.html): a RateLimit of 1 request per second, and a BurstLimit of 2 requests per second\.

## Amazon Connect Voice ID Service API throttling quotas<a name="voiceid-api-quotas"></a>


| API | Default TPS throttling limits | 
| --- | --- | 
|  EvaluateSession  |  60  | 
|  Domain APIs: CreateDomain, DescribeDomain, UpdateDomain, DeleteDomain, ListDomains Batch APIs: StartSpeakerEnrollmentJob, DescribeSpeakerEnrollmentJob, ListSpeakerEnrollmentJobs, StartFraudsterRegistrationJob, DescribeFraudsterRegistrationJob, ListFraudsterRegistrationJobs  |  2  | 
|  ListSpeakers  |  5  | 
|  DescribeSpeaker, OptOutSpeaker, DeleteSpeaker, DescribeFraudster, DeleteFraudster  |  10  | 
|  CreateIntegrationAssociation, DeleteIntegrationAssociation, ListIntegrationAssociation  |  2  | 
|  TagResource, UnTagResource, ListTagsForResource  |  2  | 