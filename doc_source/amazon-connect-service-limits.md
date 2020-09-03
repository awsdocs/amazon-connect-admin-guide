# Amazon Connect service quotas<a name="amazon-connect-service-limits"></a>

**All service quotas can be adjusted/increased unless otherwise noted\.**
+ To submit a service quota increase, use the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.
+ Use the same form to submit a request to port your US phone number from your current carrier to Amazon Connect\. For more information about porting phone numbers, see [Port your current phone number](port-phone-number.md)\.


| Item | Default quotas for new accounts created February, 2020 or later\. [Learn more](#default-quotas) | 
| --- | --- | 
|  AWS Lambda functions per instance  |  35  | 
|  Agent status per instance  |  50 This quota cannot be increased\.  | 
|  Amazon Connect instances per account  |  2  | 
|  Amazon Lex bots per instance  |  50  | 
|  Concurrent calls per instance  |  10 If this quota is exceeded, contacts will get a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.   You can calculate your configured quota using CloudWatch metrics\. For instructions, see [Use CloudWatch metrics to calculate concurrent call quota](monitoring-cloudwatch.md#connect-cloudwatch-concurrent-call-quota)\.  Or, edit a queue and enter an exceptionally large number for the contact limit\. The resulting error message will display your quota\. For example, in the following image, it shows the quota for that instance is 99\. ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/concurrent-call-quota.png)   | 
|  Concurrent chats per instance  |  100 This includes chats that are waiting\. If this quota is exceeded, the API call fails with a quota exceeded error\.  | 
|  Contact flows per instance  |  100  | 
|  Hours of operation per instance  |  100  | 
|  Phone numbers per instance  |  5  | 
|  Prompts per instance  |  500  | 
|  Queues per instance  |  50  | 
|  Queues per routing profile per instance  |  50 This quota refers to number of queue/channel combinations per routing profile\. For example, in the following image there are two queues, but there are three queue\-channel combinations: BasicQueue\-Voice, BasicQueue\-Chat, and Queue10\-Voice\. This counts three towards the service limit of 50\. ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-queue-channel-combinations.png)  | 
|  Quick connects per instance  |  100  | 
|  Rate of API requests  |  See [Amazon Connect API throttling quotas](#connect-api-quotas)\.  | 
|  Reports per instance  |  500 Personal saved reports count towards the reports per instance\. For example, if one of your supervisors saves a report every day, it will count towards your overall number of saved reports per instance\. As a best practice, we recommend you implement policies so reports don't pile up\.   | 
|  Routing profiles per instance  |  100  | 
|  Scheduled reports per instance  |  50  | 
|  Security profiles per instance  |  100  | 
|  User hierarchy groups per instance  |  250  | 
|  Users per instance  |  500  | 

**Note**  
Amazon Connect is not available to customers in India using Amazon Web Services through Amazon Internet Services Pvt\. Ltd \(AISPL\)\. You will receive an error message if you try to create an instance in Amazon Connect\.

## About default quotas<a name="default-quotas"></a>

The preceding table provides the default quotas for new Amazon Connect accounts as of February 2020\. Because the quotas have been adjusted over time, the quotas in place for your account may be different than the quotas described here\.

## Feature specifications<a name="feature-limits"></a>

The following table lists feature specifications\. They cannot be increased\.


| Item | Feature Specification | 
| --- | --- | 
| People who can listen in on the same agent call at one time  |  5  | 
|  Contact Trace Record retention  |  24 months from the time the associated contact was initiated\.  You can choose to stream CTRs to Kinesis so you can manage retention and perform advanced analysis\.  | 
|  Max size of the CTR attributes section  |  32KB   | 
|  Active chats per agent  |  5  | 
|  Total duration per chat  |  25 hours, including wait time  | 
|  Characters per chat message  |  1024  | 

## Countries you can call<a name="country-code-allow-list"></a>

You can place calls to the following countries when you create a new instance\.

If you already have an instance, the countries that you are allowed to call may be different that those listed in the following table because we have changed the service quotas over time\.


| Item | Default quota | 
| --- | --- | 
| Country code allow list for Outbound Calls |  [Submit a service quota increase request](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect) to allow calling to additional countries, or to limit the countries that you can call from\. You must be signed in to your AWS account to access the form\. For a list of all the countries available for outbound calling, see [Amazon Connect pricing](http://aws.amazon.com/connect/pricing/)\.  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-service-limits.html)  | 

† UK numbers with a 447 prefix are not allowed by default\. Before you can dial these UK mobile numbers, you must submit a service quota increase request\.

## Amazon Connect API throttling quotas<a name="connect-api-quotas"></a>

Amazon Connect throttling quotas are by account, not by user and not by instance\. For example: 
+ If different IAM users from the same account make requests, they are sharing a throttle bucket\. 
+ If multiple requests are sent from different instances from the same account, they are also sharing a throttle bucket\. 

 When you use the [Amazon Connect Service API ](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html), the number of requests per second is limited to the following:
+ For the [GetMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricData.html) and [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) operations, a RateLimit of 5 requests per second, and a BurstLimit of 8 requests per second\.
+ For all other operations, a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.

## Amazon Connect Participant Service API throttling quotas<a name="connect-participant-api-quotas"></a>

For the Amazon Connect Participant Service, the quotas are by instance\.

 When you use the [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html), the number of requests per second is limited to the following:
+  [CreateParticipantConnection](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateParticipantConnection.html), [DisconnectParticipant](https://docs.aws.amazon.com/connect/latest/APIReference/API_DisconnectParticipant.html), and [GetTranscript](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetTranscript.html): a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.
+  [SendEvent](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendEvent.html) and [SendMessage](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendMessage.html): a RateLimit of 10 requests per second, and a BurstLimit of 15 requests per second\.