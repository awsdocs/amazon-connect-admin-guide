# Amazon Connect Service Limits<a name="amazon-connect-service-limits"></a>

The following table provides the default limits for new Amazon Connect instances\. Because the limits have been adjusted over time, the limits in place for your account may be different than the limits described here\. There may even be differences between the instances created for your account\. For example, if you created an instance when the default limit for concurrent active calls was 10, the limit is 10 concurrent active calls\. If you create a new instance today, the limit for the instance is 100 concurrent active calls\. For API request limits, see [Amazon Connect API Throttling Limits](#connect-api-limits)

To start, you can create five instances per AWS account in each of AWS Regions where Amazon Connect is available\. If you need more instances, or a change to a service limit, request a change using the [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.

Use the same form to submit a request to port your US phone number from your current carrier to Amazon Connect\. For more information about porting phone numbers, see [Port Your Current Phone Number](port-phone-number.md)\.

There is also a service limit for the countries to which you can place outbound calls from your instance\. If you already have an instance, the countries that you are allowed to call may be different that those listed in the following table because we have changed the service limits over time\. You can submit a service limit increase request to allow calling to additional countries, or to limit the countries that you can call from your instance\.

**Note**  
Amazon Connect is not available to customers in India using Amazon Web Services through Amazon Internet Services Pvt\. Ltd \(AISPL\)\. You will receive an error message if you try to create an instance in Amazon Connect\.


| Item | Default limit | 
| --- | --- | 
|  Amazon Connect instances per account  |  5  | 
|  Users per instance  |  500  | 
|  Phone numbers per instance  |  10  | 
|  Queues per instance  |  50  | 
|  Queues per routing profile  |  50  | 
|  Routing profiles per instance  |  100  | 
|  Hours of operation per instance  |  100  | 
|  Quick connects per instance  |  100  | 
|  Prompts per instance  |  500  | 
|  Agent status per instance  |  50 This limit cannot be increased\.  | 
|  Security profiles per instance  |  100  | 
|  Contact flows per instance  |  100  | 
|  Agent hierarchy groups per instance  |  50  | 
|  Reports per instance  |  500  | 
|  Scheduled reports per instance  |  50  | 
|  Concurrent active calls per instance  |  100\. If this is exceeded, contacts will get a reorder tone \(aka fast busy tone\), which indicates no transmission path to the called number is available\.   | 
| Phone Number Porting |  You can port your US phone numbers from your current carrier to Amazon Connect\. For information about how to port your phone number, see [Port Your Current Phone Number](port-phone-number.md)\.  | 
| Country code whitelisting for Outbound Calls | You can place calls to the following dialing codes when you create a new instance: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-service-limits.html)  | 

† UK numbers with a 447 prefix are not allowed by default\. Before you can dial these UK mobile numbers, you must submit a service limit increase request\.

## Amazon Connect API Throttling Limits<a name="connect-api-limits"></a>

When you use the Amazon Connect API, the number of requests per second is limited to the following:
+ For the `GetMetricData` and `GetCurrentMetricData` operations, a RateLimit of 5 requests per second, and a BurstLimit of 8 requests per second\.
+ For all other operations, a RateLimit of 2 requests per second, and a BurstLimit of 5 requests per second\.