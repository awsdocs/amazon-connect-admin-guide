# Amazon Connect Service Quotas<a name="amazon-connect-service-limits"></a>

The following table provides the default quotas for new Amazon Connect accounts as of February 2020\. Because the quotas have been adjusted over time, the quotas in place for your account may be different than the quotas described here\. 

**All service quotas can be adjusted/increased unless otherwise noted\.**
+ To submit a service quota increase, use the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.
+ Use the same form to submit a request to port your US phone number from your current carrier to Amazon Connect\. For more information about porting phone numbers, see [Port Your Current Phone Number](port-phone-number.md)\.


| Item | Default quota | 
| --- | --- | 
|  Amazon Connect instances per account  |  2  | 
|  Users per instance  |  500  | 
|  Phone numbers per instance  |  5  | 
|  Queues per instance  |  50  | 
|  Queues per routing profile  |  50  | 
|  Routing profiles per instance  |  100  | 
|  Hours of operation per instance  |  100  | 
|  Quick connects per instance  |  100  | 
|  Prompts per instance  |  500  | 
|  Agent status per instance  |  50 This quota cannot be increased\.  | 
|  Security profiles per instance  |  100  | 
|  Contact flows per instance  |  100  | 
|  Agent hierarchy groups per instance  |  250  | 
|  Reports per instance  |  500 Personal saved reports count towards the reports per instance\. For example, if one of your supervisors saves a report every day, it will count towards your overall number of saved reports per instance\. As a best practice, we recommend you implement policies so reports don't pile up\.   | 
| Managers who can listen in on an agent call at the same time  |  5 This quota cannot be increased\.  | 
|  Scheduled reports per instance  |  50  | 
|  Contact Trace Record retention  |  24 months from the time the associated contact was initiated\. This quota cannot be increased\.  You can choose to stream CTRs to Kinesis so you can manage retention and perform advanced analysis\.  | 
|  Lambda functions  |  35 functions per Amazon Connect instance  | 
|  Amazon Lex bots  |  50 Amazon Lex bots per Amazon Connect instance  | 
|  Concurrent chats per instance  |  100\. This includes chats that are waiting\. If this is exceeded, the API call fails with a quota exceeded error\.  | 
|  Active chats per agent  |  5 This quota cannot be increased\.  | 
|  Total duration per chat  |  25 hours, including wait time This quota cannot be increased\.  | 
|  Characters per chat message  |  1024 This quota cannot be increased\.  | 
|  Concurrent calls per instance  |  5\. If this is exceeded, contacts will get a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.   | 
|  Call per second  |  1   | 
| Phone Number Porting |  You can port your US phone numbers from your current carrier to Amazon Connect\. For information about how to port your phone number, see [Port Your Current Phone Number](port-phone-number.md)\.  | 

**Note**  
Amazon Connect is not available to customers in India using Amazon Web Services through Amazon Internet Services Pvt\. Ltd \(AISPL\)\. You will receive an error message if you try to create an instance in Amazon Connect\.

## Countries You Can Call<a name="country-code-allow-list"></a>

You can place calls to the following countries when you create a new instance\.

If you already have an instance, the countries that you are allowed to call may be different that those listed in the following table because we have changed the service quotas over time\.


| Item | Default quota | 
| --- | --- | 
| Country code allow list for Outbound Calls |  [Submit a service quota increase request](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect) to allow calling to additional countries, or to limit the countries that you can call from\. You must be signed in to your AWS account to access the form\. For a list of all the countries available for outbound calling, see [Amazon Connect pricing](http://aws.amazon.com/connect/pricing/)\.  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-service-limits.html)  | 

† UK numbers with a 447 prefix are not allowed by default\. Before you can dial these UK mobile numbers, you must submit a service quota increase request\.

## Amazon Connect API Throttling Quotas<a name="connect-api-limits"></a>

Amazon Connect throttling quotas are by account, not by user and not by instance\. For example: 
+ If different IAM users from the same account make requests, they are sharing a throttle bucket\. 
+ If multiple requests are sent from different instances from the same account, they are also sharing a throttle bucket\. 

 When you use the [Amazon Connect Service API ](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html), the number of requests per second is limited to the following:
+ For the [GetMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricData.html) and [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) operations, a RateLimit of 5 requests per second, and a BurstLimit of 8 requests per second\. These quotas cannot be increased\. 
+ For all other operations, a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.

 When you use the [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html), the number of requests per second is limited to the following:
+  [CreateParticipantConnection](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateParticipantConnection.html), [DisconnectParticipant](https://docs.aws.amazon.com/connect/latest/APIReference/API_DisconnectParticipant.html), and [GetTranscript](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetTranscript.html): a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.
+  [SendEvent](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendEvent.html) and [SendMessage](https://docs.aws.amazon.com/connect/latest/APIReference/API_SendMessage.html): a RateLimit of 10 requests per second, and a BurstLimit of 15 requests per second\.