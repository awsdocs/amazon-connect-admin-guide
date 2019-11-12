# CloudWatch Metrics for Your Amazon Connect Instance<a name="monitoring-cloudwatch"></a>

Amazon Connect sends data about your instance to CloudWatch metrics so that you can collect, view, and analyze CloudWatch metrics for your Amazon Connect virtual contact center\. You can use this data to monitor key operational metrics and set up alarms\. Data about your contact center is sent to CloudWatch every 1 minute\.

When you view the CloudWatch metrics dashboard, you can specify the refresh interval for the data displayed\. The values displayed in the dashboard reflect the values for the refresh interval you define\. For example, if you set the refresh interval to 1 minute, the values displayed are for a minute period\. You can select a refresh interval of 10 seconds, but Amazon Connect does not send data more often than every 1 minute\. Metrics that are sent to CloudWatch are available for two weeks, and then discarded\. To learn more about metrics in CloudWatch, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\.

## Amazon Connect Metrics Sent to CloudWatch<a name="connect-metrics-cloudwatch"></a>

The `AWS/Connect` namespace includes the following metrics\.

**CallsBreachingConcurrencyQuota**  
The number of voice calls that exceeded the concurrent active calls limit for the instance\. This is a count of the number of calls that exceeded the limit, not the number of concurrent calls in excess of the limit\.  
Unit: Count  
Dimension:  
+ **InstanceId**: The ID of your instance

**CallBackNotDialableNumber**  
The number of times a queued callback to a customer could not be dialed because the customer's number is in a country for which outbound calls are not allowed for the instance\. The countries allowed for an instance are defined by the service limits\.  
Unit: Count  
Dimensions:  
+ **InstanceId** The ID of your instance
+ **MetricGroup**: **ContactFlow**
+ **ContactFlowName**: The name of your contact flow

**CallRecordingUploadError**  
The number of call recordings that failed to upload to the Amazon S3 bucket configured for your instance\. This is the bucket specified in **Data Storage** > **Call Recordings** settings for the instance\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **CallRecordings**

**CallsPerInterval**  
The number of voice calls, both inbound and outbound, received or placed per second in the instance\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ConcurrentCalls**  
The number of concurrent active voice calls in the instance at the time the data is displayed in the dashboard\. The value displayed for this metric is the number of concurrent active calls at the time the dashboard is displayed, and not a sum for the entire interval of the refresh interval set\. All active voice calls are included, not only active calls that are connected to agents\.  
While all statistics are available in CloudWatch for concurrent voice calls you might be most interested in looking at the Maximum/Average statistic\. The Sum statistic isn't as useful here\.   
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ConcurrentCallsPercentage**  
The percentage of the concurrent active voice calls service limit used in the instance\. This is calculated by `ConcurrentCalls/ConfiguredConcurrentCallsLimit * 100`\.  
Unit: Percent  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ContactFlowErrors**  
The number of times the error branch for a contact flow was executed\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **ContactFlow**
+ **ContactFlowName**: The name of your contact flow

**ContactFlowFatalErrors**  
The number of times a contact flow failed to execute due to a system error\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **ContactFlow**
+ **ContactFlowName**: The name of your contact flow

**LongestQueueWaitTime**  
The longest amount of time, in seconds, that a contact waited in a queue\. This is the length of time a contact waited in a queue during the refresh interval selected in the CloudWatch dashboard, such as 1 minute or 5 minutes\.  
Unit: Seconds  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Queue**
+ **QueueName**: The name of your queue

**MissedCalls**  
The number of voice calls that were missed by agents during the refresh interval selected, such as 1 minute or 5 minutes\. A missed call is one that is not answered by an agent within 20 seconds\.  
To monitor the total missed calls in a given time period, take a look at the Sum statistic in CloudWatch\.  
Unit: Seconds  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**MisconfiguredPhoneNumbers**  
The number of calls that failed because the phone number is not associated with a contact flow\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**PublicSigningKeyUsage**  
The number of times a contact flow security key \(public signing key\) was used to encrypt customer input in a contact flow\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **SigningKeyId**: The ID of yoru signing key

**QueueCapacityExceededError**  
The number of calls that were rejected because the queue was full\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Queue**
+ **QueueName**: The name of your queue

**QueueSize**  
The number of contacts in the queue\. The value reflects the number of contacts in the queue at the time the dashboard is accessed, not for the duration of the reporting interval\.  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **Queue**
+ **QueueName**: The name of your queue

**ThrottledCalls**  
The number of voice calls that were rejected because the rate of calls per second exceeded the maximum supported limit\. To increase the supported rate of calls, request an increase in the service limit for concurrent active calls per instance\.  
To monitor the total throttled calls in a given time period, take a look at the Sum statistic in CloudWatch\.  
Unit: Seconds  
Unit: Count  
Dimensions:  
+ **InstanceId**: The ID of your instance
+ **MetricGroup**: **VoiceCalls**

**ToInstancePacketLossRate**  
The ratio of packet loss for calls in the instance, reported every 10 seconds\. Each data point is between 0 and 1, which represents the ratio of packets lost for the instance\.  
Unit: Percent  
Dimensions:  
+ **Participant**: **Agent**
+ **Type of Connection**: **WebRTC**
+ **Instance ID**: The ID of your instance
+ **Stream Type**: **Voice**

## Amazon Connect CloudWatch Metrics Dimensions<a name="connect-cloudwatch-dimensions"></a>

In CloudWatch, a dimension is a name/value pair that uniquely identifies a metric\. In the dashboard, metrics are grouped by dimension\. The following dimensions are used in the CloudWatch dashboard for Amazon Connect metrics\. When you view metrics in the dashboard, only metrics with data are displayed\. If there is no activity during the refresh interval for which there is a metric, then no data from your instance is displayed in the dashboard\. The following dimensions are used for Amazon Connect metrics in CloudWatch\.

### Contact Flow Metrics Dimension<a name="contact-flow-dimension"></a>

Filters metric data by contact flow\. Includes the following metrics:
+ CallRecordingUploadError
+ ContactFlowErrors
+ ContactFlowFatalErrors
+ MisconfiguredPhoneNumbers
+ PublicSigningKeyUsage

### Instance Metrics Dimension<a name="instance-metrics-dimension"></a>

Filters meta data by instance\. Includes the following metrics:
+ CallsBreachingConcurrencyQuota
+ CallsPerInterval
+ ConcurrentCalls
+ ConcurrentCallsPercentage
+ MissedCalls
+ ThrottledCalls

### Instance ID, Participant, Stream Type, Type of Connection<a name="stream-type-dimension"></a>

Filters metric data by connection\. Includes the following metrics:
+ ToInstancePacketLossRate

### Queue Metrics Dimension<a name="queue-metrics-dimension"></a>

**Note**  
If a queue has a dimension name in non\-ASCII characters, you won't be able to see it in CloudWatch\. 

Filters metric data by queue\. Includes the following metrics:
+ CallBackNotDialableNumber
+ LongestQueueWaitTime
+ QueueCapacityExceededError
+ QueueSize