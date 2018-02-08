# Monitoring Amazon Connect Using Amazon CloudWatch Metrics<a name="monitoring-cloudwatch"></a>

Amazon Connect integrates with CloudWatch so that you can collect, view, and analyze CloudWatch metrics for your Amazon Connect virtual contact center\. Using this data, you can monitor key operational metrics and set up alarms\. The metrics that you configure are automatically collected and pushed to CloudWatch every five minutes\. Metrics are archived for two weeks; after that period, the data is discarded\.

## VoiceCalls Metrics<a name="voice-call"></a>


| Metric | Description | 
| --- | --- | 
|  `MissedCalls`  |  Represents the number of voice calls that were missed by the agents \(not answered within 20 seconds\)\.  | 
|  `ThrottledCalls`  |  Represents the number of voice calls that were throttled by the Amazon Connect Voice Service due to TPS/Callrate going beyond configured threshold for the Amazon Connect instance\.  | 
|  `CallsBreachingConcurrencyQuota`  |  Represents the number of voice calls that breached the `Concurrency Quota` configured threshold for the Amazon Connect instance\.  | 
|  `ConcurrentCalls`  |  Represents the number of concurrent voice calls\.  | 
|  `ConcurrentCallsPercentage`  |  Represents the percentage of concurrent voice calls\. `ConcurrentCalls/ConfiguredConcurrentCallsLimit * 100`\.  | 
|  `CallsPerInterval`  |  Represents the rate at which voice calls \(both inbound, outbound\) are coming\.  | 

## CallRecordings Metrics<a name="call-recordings-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `CallRecordingUploadError`  |  Represents the number of call recordings that failed to be uploaded to the customer's S3 bucket\.  | 

## ContactFlow Metrics<a name="contact-flow-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `MisconfiguredPhoneNumbers`  |  Represents the number of calls that failed because the phone number is not configured to a **Contact flow**\.  | 
|  `ContactFlowFatalErrors`  |  Represents **Contact flow** execution failures\.  | 
|  `ContactFlowErrors`  |  Represents the number of times the **Contact flow** branched to an `ERROR` label in the instruction\.  | 

## Queue Metrics<a name="queue-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `QueueCapacityExceededError`  |  Represents the number of calls rejected due to the queue being full\.  | 
|  `QueueCallBackNonDialableNumber`  |  Represents an error when the queue call back to a customer number is not dialable due to dialing profile restrictions\.  | 

## Other Metrics<a name="other-metrics"></a>


| Metric | Description | 
| --- | --- | 
|  `PublicSigningKeyUsage`  |  Usage count of the public sign\-in key for CCIVR contact flows in Amazon Connect\.  | 

## Metric Dimensions<a name="connect-metric-dimensions"></a>

To filter the metrics for Amazon Connect, use the following dimensions\.


| Metric | Description | 
| --- | --- | 
|  `InstanceId`  |  The Amazon Connect instance ID\. This is currently not the complete ARN, just the ID\.  | 
|  `QueueName`  |  The name of the queue\. This dimension is relevant only for queue metrics\.  | 
|  `ContactFlowName`  |  The name of the ContactFlow\. This dimension is relevant only for ContactFlow metrics\.  | 
|  `MetricGroup`  |  The category group\. The following category groups are supported: `CallRecordings`, `ContactFlow`, `Queue`, and `VoiceCalls`\.  | 