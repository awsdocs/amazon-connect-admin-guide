# Flow block: Set recording and analytics behavior<a name="set-recording-behavior"></a>

## Description<a name="set-recording-behavior-description"></a>
+ Sets options for recording and/or monitoring \(listen\-in\) voice and chat conversations\.
+ It enables features in Contact Lens for Amazon Connect\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\.

## Supported channels<a name="set-recording-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | No \- Error branch | 

## Flow types<a name="set-recording-behavior-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer Queue flow
+ Outbound whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-recording-behavior-properties"></a>

The following image shows the **Properties** page of the **Set recording and analytics behavior** block\. It has two sections:
+ Call recording: use this section to enable or disable call recording fro the agent customer, or both\.
+ Analytics: use this section to enable Contact Lens analytics\.

![\[The properties page of the Set recording and analytics behavior block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

When configuring this block to [set up recording behavior](set-up-recordings.md), choose as follows:
+ To record voice conversations, choose what you want to record: **Agent and Customer**, **Agent only**, or **Customer only**\.
+ To record chat conversations, you need to choose **Agent and Customer**\.
+ To enable monitoring of voice and/or chat conversations, you need to choose **Agent and Customer**\.

For information about using this block to enable Contact Lens, including features such as sensitive data redaction, see [Enable Contact Lens for Amazon Connect](enable-analytics.md)\.

## Configuration tips<a name="set-recording-behavior-tips"></a>
+ Let's say you have a flow that links to a flow that links to another flow\. Each flow might have it's own **Set recording behavior** block\. The last **Set recording behavior** block overrides the settings of the previous two **Set recording behavior** blocks\. 

  For example, you might have a flow with **Set recording behavior to record Agent and Customer**\. But if the next **Set recording behavior** block is set to **Agent only**, that block overrides the behavior of the previous block\. 
+ Unchecking **Enable Contact Lens conversational analytics** does not disable Contact Lens analytics unless it is unchecked in the first **Set recording and analytics and behavior** block that appears in the flow, or predecessor flow\. 

  To disable Contact Lens conversational analytics, do one of the following: 
  + Uncheck **Enable Contact Lens conversational analytics** in the first **Set recording and analytics behavior** block that occurs in your flows\.
  + Place the **Set recording and analytics behavior** block further along in your branched flow experience, where you want to collect Contact Lens analytics\.
+ If an agent puts a customer on hold, the agent is still recorded, but the customer is not\.
+ If you want to transfer a contact to another agent or queue, and you want to continue using Contact Lens to collect data, you need to add to the flow another **Set recording behavior** block with **Enable analytics** turn on\. This is because a transfer generates a second contact ID and contact record\. Contact Lens needs to run on that contact record as well\.
+ When you enable Contact Lens, the type of flow that the block is in, and where it is placed in the flow, determine **whether** agents receive the contact summarization transcript, and **when** they receive it\. 

  For more information and example use cases that explain how the block affects the agents experience with contact summarization, see [Design a flow for call summarization](enable-analytics.md#call-summarization-agent)\.

## Configured block<a name="set-recording-behavior-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has one branch: **Success**\. 

![\[A configured Set recording and analytics behavior block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior-configured.png)

## Sample flows<a name="set-recording-behavior-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-recording-behavior-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up recording behavior](set-up-recordings.md)
+ [Set up live monitoring for voice and/or chat](monitor-conversations.md)
+ [Review recorded conversations between agents and customers using Amazon Connect](review-recorded-conversations.md)
+ [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)