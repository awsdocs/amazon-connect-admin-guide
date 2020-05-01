# Contact Block: Check Staffing<a name="check-staffing"></a>

## In contact flow types<a name="check-staffing-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Generic contact flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="check-staffing-description"></a>
+ Checks the current working queue, or queue you specify in the block, for whether agents are [available](real-time-metrics-definitions.md#available-real-time), [staffed](real-time-metrics-definitions.md#staffed-real-time), or [online](real-time-metrics-definitions.md#online-real-time)\.
+ Before transferring a call to agent and putting that call in a queue, use the **Check hours of operation** and **Check staffing** blocks\. They verify that the call is within working hours and that agents are staffed to service\.

## Properties<a name="check-staffing-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-staffing-properties.png)

## Configuration tips<a name="check-staffing-tips"></a>
+ You must set a queue before using a **Check staffing** block in your contact flow\. You can use a [Set Working Queue](set-working-queue.md) block to set the queue\.
+ If a queue is not set, the contact is routed down the **Error** branch\.
+ When a contact is transferred from one flow to another, the queue that is set in a contact flow is passed from that flow to the next flow\.

## Configured block<a name="check-staffing-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-staffing-configured.png)

## Scenarios<a name="check-staffing-scenarios"></a>

See these topics for scenarios that use this block:
+ [Transfer Contacts to a Specific Agent](transfer-to-agent.md)