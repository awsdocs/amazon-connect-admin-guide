# Contact block: Get queue metrics<a name="get-queue-metrics"></a>

## Description<a name="get-queue-metrics-description"></a>
+ Retrieves the following real\-time metrics from a queue so you can make routing decisions\. If there is no current activity in your contact center, nothing is returned for these metrics\. 
  + [Queue name](real-time-metrics-definitions.md#queue-real-time) 
  + Queue ARN\. 
  + [Contacts in queue](real-time-metrics-definitions.md#in-queue-real-time)
  + [Oldest contact in queue](real-time-metrics-definitions.md#oldest-real-time)
  + [Agents online](real-time-metrics-definitions.md#online-real-time)
  + [Agents available](real-time-metrics-definitions.md#available-real-time)
  + [Agents staffed](real-time-metrics-definitions.md#staffed-real-time)
  + [Agents after contact work](real-time-metrics-definitions.md#aftercallwork-real-time)
  + [Agents busy](real-time-metrics-definitions.md#on-call-real-time)
  + [Agents missed](real-time-metrics-definitions.md#agent-non-response-real-time) \(Agent non\-response\)
  + [Agents non\-productive](real-time-metrics-definitions.md#non-productive-time-real-time)
+ You can choose to return metrics by channel, for example, voice or chat\. You can also filter by queue or agent\. These options enable you to know how many chat and voice contacts are in a queue and if you have agents available to handle those contacts\. 
+ You can route contacts based on queue status, such as number of contacts in queue or agents available\. Queue metrics are aggregated across all channels and are returned as attributes\. The current queue is used by default\.
+ After a **Get queue metrics** block, use a [Check contact attributes](check-contact-attributes.md) to check metric values and define routing logic based on them, such as number of contacts in a queue, number of available agents, and oldest contact in a queue\. 

## Supported channels<a name="get-queue-metrics-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Contact flow types<a name="get-queue-metrics-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="get-queue-metrics-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-properties1.png)

You can retrieve metrics by channel, and/or by queue or agent\.
+ If you don't specify a channel, it returns metrics for all channels\. 
+ If you don't specify a queue, it returns metrics for the current queue\.
+ Dynamic attributes can only return metrics for one channel\. 

For example, if you choose the following settings, **Get queue metrics** would return metrics for only the BasicQueue, filtered to include only chat contacts\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-properties3.png)

## Configuration tips<a name="get-queue-metrics-tips"></a>

### Specifying a channel in the Set contact attributes block<a name="get-queue-metrics-tips1"></a>

Dynamic attributes can only return metrics for one channel\.

Before you use dynamic attributes in the **Get queue metrics** block, you need to set the attributes in the [Set contact attributes](set-contact-attributes.md) block, and specify which channel\.

When you set a channel dynamically using text, as shown in the following image, for the attribute value enter **Voice** or **Chat**\. This value is not case\-sensitive\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-properties2.png)

### Using the Check contact attributes block after the Get queue metrics block<a name="get-queue-metrics-tips2"></a>

After a **Get queue metrics** block, add a [Check contact attributes](check-contact-attributes.md) block to branch based on the returned metrics\. Use the following steps:

1. After **Get queue metrics**, add a **Check contact attributes** block\.

1. In the **Check contact attributes** block, set **Attribute to check** to **Queue metrics**\.

1. In the **Attributes** dropdown box, you'll see that the following queue metrics are returned by the **Get queue metrics** block\. Choose the metric that you want to use for the routing decision\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-block-returned-metrics.png)

## Configured block<a name="get-queue-metrics-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-queue-metrics-configured.png)

## Scenarios<a name="get-queue-metrics-scenarios"></a>

See these topics for scenarios that use this block:
+ [How to reference contact attributes](how-to-reference-attributes.md)