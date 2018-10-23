# Monitoring Amazon Connect in Amazon CloudWatch Metrics<a name="monitoring-cloudwatch"></a>

Amazon Connect sends data about your instance to CloudWatch metrics so that you can collect, view, and analyze CloudWatch metrics for your Amazon Connect virtual contact center\. You can use this data to monitor key operational metrics and set up alarms\. Data about your contact center is sent to CloudWatch every 1 minute\.

When you view the CloudWatch metrics dashboard, you can specify the refresh interval for the data displayed\. The values displayed in the dashboard reflect the values for the refresh interval you define\. For example, if you set the refresh interval to 1 minute, the values displayed are for a minute period\. You can select a refresh interval of 10 seconds, but Amazon Connect does not send data more often than every 1 minute\. Metrics that are sent to CloudWatch are available for two weeks, and then discarded\. To learn more about metrics in CloudWatch, see [What is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)

## Amazon Connect Metrics Sent to CloudWatch<a name="connect-metrics-cloudwatch"></a>

The following Amazon Connect metrics are sent to CloudWatch:
+ **CallsBreachingConcurrencyQuota**—The number of voice calls that exceeded the concurrent active calls limit for the instance\. This is a count of the number of calls that exceeded the limit, not the number of concurrent calls in excess of the limit\.
+ **CallBackNotDialableNumber**—The number of times a queued call back to a customer could not be dialed because the customer's number is in a country for which outbound calls are not allowed for the instance\. The countries allowed for an instance are defined by the service limits\.
+ **CallRecordingUploadError**—The number of call recordings that failed to upload to the Amazon S3 bucket configured for your instance\. This is the bucket specified in **Data Storage** > **Call Recordings** settings for the instance\.
+ **CallsPerInterval**—The number of voice calls, both inbound and outbound, received or placed per second in the instance\.
+ **ConcurrentCalls**—The number of concurrent active voice calls in the instance at the time the data is displayed in the dashboard\. The value displayed for this metric is the number of concurrent active calls at the time the dashboard is displayed, and not a sum for the entire interval of the refresh interval set\. All active voice calls are included, not only active calls that are connected to agents\.
+ **ConcurrentCallsPercentage**—The percentage of the concurrent active voice calls service limit used in the instance\. This is calculated by `ConcurrentCalls/ConfiguredConcurrentCallsLimit * 100`\.
+ **ContactFlowErrors**—The number of times the error branch for a contact flow was executed\.
+ **ContactFlowFatalErrors**—The number of times a contact flow failed to execute due to a system error\.
+ **LongestQueueWaitTime**—The longest amount of time, in seconds, that a contact waited in a queue\. This is the length of time a contact waited in a queue during the refresh interval selected in the CloudWatch dashboard, such as 1 minute or 5 minutes\.
+ **MissedCalls**—The number of voice calls that were missed by agents during the refresh interval selected, such as 1 minute or 5 minutes\. A missed call is one that is not answered by an agent within 20 seconds\.
+ **MisconfiguredPhoneNumbers**—The number of calls that failed because the phone number is not associated with a contact flow\.
+ **PublicSigningKeyUsage**—The number of times a contact flow security key \(public signing key\) was used to encrypt customer input in a contact flow\.
+ **QueueCapacityExceededError**—The number of calls that were rejected because the queue was full\.
+ **QueueSize**—The number of contacts in the queue\. The value reflects the number of contacts in the queue at the time the dashboard is accessed, not for the duration of the reporting interval\.
+ **ThrottledCalls**—The number of voice calls that were throttled by the Amazon Connect service because the rate of calls per second \(Callrate\) exceeded the configured limit for the instance\.
+ **ToInstancePacketLossRate**—The ratio of packet loss for calls in the instance, reported every 10 seconds\. Each data point is between 0 and 1, which represents the ratio of packets lost for the instance\.

## Amazon Connect CloudWatch Metrics Dimensions<a name="connect-cloudwatch-dimensions"></a>

In CloudWatch, a dimension is a name/value pair that uniquely identifies a metric\. In the dashboard, metrics are grouped under dimensions\. The following dimensions are used in the CloudWatch dashboard for Amazon Connect metrics\. When you view metrics, only metrics for which there is data are displayed in the dashboard\. If there is no activity during the refresh interval for which there is a metric, then no data from your instance is displayed in the dashboard\. The following dimensions are used for Amazon Connect metrics in CloudWatch\.

## Instance ID, Participant, Stream Type, Type of Connection<a name="stream-type-dimension"></a>

This dimension contains metrics about connections to your instance, and includes:
+ ToInstancePacketLossRate

## Contact Flow Metrics Dimension<a name="contact-flow-dimension"></a>

This dimension contains metrics about contact flows in your instance, and includes:
+ CallRecordingUploadError
+ ContactFlowErrors
+ ContactFlowFatalErrors
+ MisconfiguredPhoneNumbers
+ PublicSigningKeyUsage

## Queue Metrics Dimension<a name="queue-metrics-dimension"></a>

This dimension contains metrics about queues in your instance, and includes:
+ CallBackNotDialableNumber
+ LongestQueueWaitTime
+ QueueCapacityExceededError
+  QueueSize 

## Instance metrics Dimension<a name="instance-metrics-dimension"></a>

This dimension contains metrics about voice calls and call recordings in your instance, and includes:
+ CallsBreachingConcurrencyQuota
+ CallsPerInterval
+ ConcurrentCalls
+ ConcurrentCallsPercentage
+ MissedCalls
+ ThrottledCalls 