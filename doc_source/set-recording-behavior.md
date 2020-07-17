# Contact block: Set recording and analytics behavior<a name="set-recording-behavior"></a>

## Contact flow types<a name="set-recording-behavior-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="set-recording-behavior-description"></a>
+ Sets options for recording and/or monitoring \(listen\-in\) voice and chat conversations\.
+ If you've signed up for the [Contact Lens for Amazon Connect](enable-analytics.md) preview, it enables analytics for that contact flow\. To use Contact Lens for Amazon Connect you also need to enable it as the instance level\. For instructions, see [Update instance settings](update-instance-settings.md)\.

## Properties<a name="set-recording-behavior-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

When configuring this block to [set up recording behavior](set-up-recordings.md), choose as follows:
+ To record voice conversations, choose what you want to record: **Agent and Customer**, **Agent only**, or **Customer only**\.
+ To record chat conversations, you need to choose **Agent and Customer**\.
+ To enable monitoring of voice and/or chat conversations, you need to choose **Agent and Customer**\.

If you've signed up for the Contact Lens for Amazon Connect preview, choose **Agent and Customer**\.

Also choose **Enable analytics**\. If you don't see this option, Contact Lens for Amazon Connect hasn't been enabled for your instance\. To enable it, see [Update instance settings](update-instance-settings.md)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior2.png)

## Configuration tips<a name="set-recording-behavior-tips"></a>
+ Let's say you have a flow that links to a flow that links to another flow\. Each flow might have it's own **Set recording behavior** block\. The last **Set recording behavior** block overrides the settings of the previous two **Set recording behavior** blocks\. 

  For example, you might have a contact flow with **Set recording behavior to record Agent and Customer**\. But if the next **Set recording behavior** block is set to **Agent only**, that block overrides the behavior of the previous block\. 
+ If an agent puts a customer on hold, the agent is still recorded, but the customer is not\.
+ If you want to transfer a contact to another agent or queue, and you want to continue using Contact Lens to collect data, you need to add to the flow another **Set recording behavior** block with **Enable analytics** turn on\. This is because a transfer generates a second contact ID and CTR\. Contact Lens needs to run on that CTR as well\.

## Configured block<a name="set-recording-behavior-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior-configured.png)

## Sample flows<a name="set-recording-behavior-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-recording-behavior-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up recording behavior](set-up-recordings.md)
+ [Monitor live conversations](monitor-conversations.md)
+ [Review recorded conversations](review-recorded-conversations.md)
+ [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)