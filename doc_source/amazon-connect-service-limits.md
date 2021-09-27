# Amazon Connect service quotas<a name="amazon-connect-service-limits"></a>

**All service quotas can be adjusted/increased unless otherwise noted\.**
+ Create your instance \(it must exist\) and then submit a service quota increase\. Use the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.
+ It can take up to a few weeks to increase your service quota\. If you're increasing your quotas as part of a larger project, be sure to add this time to your plan\.
+ Use the same form to submit a request to port your US phone number from your current carrier to Amazon Connect\. For more information about porting phone numbers, see [Port your current phone number](port-phone-number.md)\.


| Item | Default quotas for new accounts created October, 2020 or later\. [Learn more](#default-quotas) | 
| --- | --- | 
|  AWS Lambda functions per instance  |  35  | 
|  Agent status per instance  |  50 This quota cannot be increased\.  | 
|  Amazon Connect instances per account  |  2  | 
|  Amazon Lex bots per instance  |  50  | 
|  Amazon Lex V2 bot aliases per instance  |  100  | 
|  Concurrent active calls per instance   |  10  **What is counted?** All calls currently being handled by agents or waiting in a queue for an agent\. Callbacks waiting in a callback queue are not counted until the callback is offered to an available agent\. If this quota is exceeded, contacts will get a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.   You can calculate your configured quota using CloudWatch metrics\. For instructions, see [Use CloudWatch metrics to calculate concurrent call quota](monitoring-cloudwatch.md#connect-cloudwatch-concurrent-call-quota)\.  **If you're only taking calls**: Another way to determine your concurrent calls quota is to edit a queue and enter an exceptionally large number for the contact limit\. The resulting error message will display your quota for concurrent calls\. For example, in the following image, it shows the call quota for that instance is 99\. ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/concurrent-call-quota.png)   | 
|  Concurrent active chats per instance  |  100 This includes chats that are waiting\. If this quota is exceeded, the API call fails with a quota exceeded error\. By default [Maximum contacts in queue](set-maximum-queue-limit.md) is set to your **Concurrent calls per instance** quota\. If you plan to have more chats than that in a queue, submit a request to increase the **Active chats per instance** quota, and then increase the [Maximum contacts in queue](set-maximum-queue-limit.md) setting\.   | 
|  Concurrent active tasks per instance  |  2500 concurrent active tasks **What is counted?** All tasks that have not yet ended are considered active and are counted as concurrent tasks: tasks that are being routed in flows, waiting in a queue for an agent, being handled by agents, or being run in After Contact Work \(ACW\)\. By default [Maximum contacts in queue](set-maximum-queue-limit.md) is set to your **Concurrent calls per instance** quota\. If you plan to have more tasks than that in a queue, submit a request to increase the **Active tasks per instance** quota, and then increase the [Maximum contacts in queue](set-maximum-queue-limit.md) setting\.   | 
|  Contact flows per instance  |  100  | 
|  Hours of operation per instance  |  100  | 
|  Phone numbers per instance  |  5  | 
|  Prompts per instance  |  500  | 
|  Queues per instance  |  50  | 
|  Queues per routing profile per instance  |  50 This quota refers to number of queue/channel combinations per routing profile\. For example, in the following image there are two queues, but there are three queue\-channel combinations: Escalation queue Voice, Escalation queue Chat, and BasicQueue Voice\. This counts three towards the service limit of 50\. ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-queue-channel-combinations.png)  | 
|  Quick connects per instance  |  100  | 
|  Rate of API requests  |  See [Amazon Connect API throttling quotas](#connect-api-quotas)\.  | 
|  Reports per instance  |  2000 Personal saved reports count towards the reports per instance\. For example, if one of your supervisors saves a report every day, it will count towards your overall number of saved reports per instance\. As a best practice, we recommend you implement policies so reports don't pile up\.   | 
|  Routing profiles per instance  |  100  | 
|  Scheduled reports per instance  |  50 This quota cannot be increased\.  | 
|  Security profiles per instance  |  100  | 
|  User hierarchy groups per instance  |  500 This quota applies to the total number of hierarchy groups you have, across all levels\. There is no feature limit for how many hierarchy groups you can have for each level\. For example, one level could have 500 hierarchy groups, which would reach the quota for your instance\.  | 
|  Users per instance  |  500  | 

**Note**  
Amazon Connect is not available to customers in India using Amazon Web Services through Amazon Internet Services Pvt\. Ltd \(AISPL\)\. You will receive an error message if you try to create an instance in Amazon Connect\.

## Amazon Connect Customer Profiles service quotas<a name="customer-profiles-quotas"></a>


| Item | Default quotas  | 
| --- | --- | 
|  Amazon Connect Customer Profiles domains count  |  100  | 
|  Keys per object type  |  10  | 
|  Maximum expiration in days  |  1,096 \(3 years\) This is the expiration of objects and profiles\.  | 
|  Maximum number of integrations  |  50  | 
|  Maximum size of all objects for a profile  |  5MB  | 
|  Object and profile maximum size  |  250KB This quota cannot be increased\.   | 
|  Objects per domain  |  100  | 
|  Objects per profile  |  100 This is the maximum number of objects that can be attached to a profile\.  | 

## Amazon Connect Voice ID service quotas<a name="voiceid-quotas"></a>


| Item | Default quotas  | 
| --- | --- | 
|  Assistants  |  3 This quota applies per account\.  | 
|  Knowledge bases  |  10  | 
|  Maximum size of a knowledge base  |  5GB per knowledge base Concurrent active sessions per domain  | 
|  Maximum number of fraudsters per domain  |  500  | 
|  Content per knowledge base  |  10,000  | 
|  Maximum size per document  |  10MB  | 
|  RateLimit for all APIs  |  50TPS  | 
|  Maximum number of speakers per domain  |  100,000  | 
|  Active Batch Speaker Enrollment Jobs per domain  |  1  | 
|  Active Batch Fraudster Registration Jobs per domain  |  1  | 
|  Speakers per Batch Speaker Enrollment Job  |  10,000  | 
|  Fraudsters per Batch Fraudster Registration Job  |  500  | 

## About default quotas<a name="default-quotas"></a>

The preceding tables that lists service quotas provides the default quotas for new Amazon Connect accounts as of February 2020\. Because the quotas have been adjusted over time, the quotas in place for your account may be different than the quotas described here\.

## Feature specifications<a name="feature-limits"></a>

The following table lists feature specifications\. They cannot be increased\.


| Item | Feature Specification | 
| --- | --- | 
| File types supported for chat attachments |  \.pdf, \.jpg, \.jpeg, \.png, \.doc, \.docx, \.xls, \.csv, \.wav, \.pptx, \.ppt, \.txt  | 
| Max file size for a chat attachment |  20MB  | 
| Attachments per chat conversation |  5  | 
| People who can listen in on the same agent call at the same time  |  5 For example, you can have a group of 5 people listen in to a call at the same time, and then a different group of 5 people listen in to a different call at the same time, and so on\.   | 
| Participants on a conference call |  3 The three participants are the customer, agent, and a third person who can be either another agent or an external third\-party\.  | 
|  Contact Trace Record retention  |  24 months from the time the associated contact was initiated\.  You can choose to stream CTRs to Kinesis so you can manage retention and perform advanced analysis\.  | 
|  Max size of the CTR attributes section  |  32KB   | 
|  Active chats per agent  |  10  | 
|  Total duration per chat  |  25 hours, including wait time  | 
|  Characters per chat message  |  1024  | 
|  Open websocket connections per chat participant  |  5  | 
|  Maximum duration of a task  |  7 days  | 
|  Maximum number of transfers for a task  |  11 transfers  | 
|  Maximum number of linked tasks on an existing contact  |  11  | 
|  Limit on creating and deleting instances  | 100 instances can be created or deleted in 30 days Amazon Connect enforces a limit on the **total** number of instances that you can create and delete in 30 days\. If you exceed this limit, you will get an error message indicating there has been an excessive number of attempts at creating or deleting instances\. You must wait 30 days before you can restart creating and deleting instances in your account\. For example, if you create 80 instances and delete 20 over the course of 30 days, you must wait an additional 30 days before you can create or delete any more instances\. If you create and delete the same instance 100 times in 30 days, the limit also applies\.   | 

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

Amazon Connect throttling quotas are by account, not by user and not by instance\. For example: 
+ If different IAM users from the same account make requests, they are sharing a throttle bucket\. 
+ If multiple requests are sent from different instances from the same account, they are also sharing a throttle bucket\. 

 When you use the [Amazon Connect Service API ](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html), the number of requests per second is limited to the following:
+ For the [GetMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricData.html) and [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) operations, a RateLimit of 5 requests per second, and a BurstLimit of 8 requests per second\.
**Note**  
The rate limit cannot be increased for GetMetricData and GetCurrentMetricData\.
+ For all other operations, a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.

## Amazon Connect Participant Service API throttling quotas<a name="connect-participant-api-quotas"></a>

For the Amazon Connect Participant Service, the quotas are by instance\.

 When you use the [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html), the number of requests per second is limited to the following:
+  [CreateParticipantConnection](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateParticipantConnection.html): a RateLimit of 6 requests per second, and a BurstLimit of 9 requests per second\.
+  [DisconnectParticipant](https://docs.aws.amazon.com/connect/latest/APIReference/API_DisconnectParticipant.html): a RateLimit of 3 requests per second, and a BurstLimit of 5 requests per second\.
+  [GetTranscript](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetTranscript.html): a RateLimit of 8 requests per second, and a BurstLimit of 12 requests per second\.
+  [SendEvent](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendEvent.html) and [SendMessage](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendMessage.html): a RateLimit of 10 requests per second, and a BurstLimit of 15 requests per second\.

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