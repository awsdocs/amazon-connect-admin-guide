# Contact Block: Get Queue Metrics<a name="get-queue-metrics"></a>

## In contact flow types<a name="get-queue-metrics-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Description<a name="get-queue-metrics-description"></a>
+ Retrieves the following real\-time metrics from a queue so you can make routing decisions:
  + [Queue name](real-time-metrics-definitions.md#queue-real-time) 
  + Queue ARN
  + [Contacts in queue](real-time-metrics-definitions.md#in-queue-real-time)
  + [Oldest contact in queue](real-time-metrics-definitions.md#oldest-real-time)
  + [Agents online](real-time-metrics-definitions.md#online-real-time)
  + [Agents available](real-time-metrics-definitions.md#available-real-time)
  + [Agents staffed](real-time-metrics-definitions.md#staffed-real-time)
  + [Agents after contact work](real-time-metrics-definitions.md#aftercallwork-real-time)
  + [Agents busy](real-time-metrics-definitions.md#on-call-real-time)
  + [Agents missed](real-time-metrics-definitions.md#agent-non-response-real-time) \(Agent non\-response\)
  + [Agents non\-productive](real-time-metrics-definitions.md#non-productive-time-real-time)
+ This block returns metrics for all media types\. You cannot return metrics for only chat or only voice, for example\.
+ You can route contacts based on queue status, such as number of contacts in queue or agents available\. Queue metrics are aggregated across all channels and are returned as attributes\. The current queue is used by default\.
+ After a **Get queue metrics** block, use a [Check Contact Attributes](check-contact-attributes.md) to check metric values and define routing logic based on them, such as number of contacts in a queue, number of available agents, and oldest contact in a queue\. 

## Properties<a name="get-queue-metrics-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-properties.png)

The following property is available:
+ **Set queue**: This is an optional parameter that lets you set the queue\. Otherwise, it uses the queue that's specified in the **Set working queue** block\. 

## Configuration tips<a name="get-queue-metrics-tips"></a>

Here's how to use the **Get queue metrics** block with the **Check contact attributes** block:

1. After **Get queue metrics**, add a **Check contact attributes** block\.

1. In the **Check contact attributes** block, set **Attribute to check** to **Queue metrics**\.

1. In the **Attributes** dropdown box, you'll see that the following queue metrics are returned by the **Get queue metrics** block\. Choose the metric that you want to use for the routing decision\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-block-returned-metrics.png)

## Configured block<a name="get-queue-metrics-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-configured.png)

## Scenarios<a name="get-queue-metrics-scenarios"></a>

See these topics for scenarios that use this block:
+ [Checking Attribute Values in a Check Contact Attributes Block](how-to-reference-attributes.md#check-contact-attrib-block)