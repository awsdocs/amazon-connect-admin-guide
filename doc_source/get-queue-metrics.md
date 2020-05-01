# Contact Block: Get Queue Metrics<a name="get-queue-metrics"></a>

## In contact flow types<a name="get-queue-metrics-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Description<a name="get-queue-metrics-description"></a>
+ Retrieve real\-time metrics from a queue so you can make routing decisions\.
+ This block returns metrics for all media types\. You cannot return metrics for only chat or only voice, for example\.
+  You can route contacts based on queue status, such as number of contacts in queue or agents available\. Queue metrics are aggregated across all channels and are returned as attributes\. The current queue is used by default\.

  Use a **Check contact attributes** block to check metric values and define routing logic based on them, such as number of contact in a queue, number of available agents, and oldest contact in a queue\. For more information, see [How to Use System Metric Attributes](attrib-system-metrics.md)\. 

## Properties<a name="get-queue-metrics-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-properties.png)

The following property is available:
+ **Set queue**: This is an optional parameter that lets you set the queue\. Otherwise, it uses the queue that's specified in the **Set working queue** block\. 

## Configured block<a name="get-queue-metrics-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-configured.png)

## Scenarios<a name="get-queue-metrics-scenarios"></a>

See these topics for scenarios that use this block:
+ [Checking Attribute Values in a Check Contact Attributes Block](how-to-reference-attributes.md#check-contact-attrib-block)