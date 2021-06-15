# Contact block: Check staffing<a name="check-staffing"></a>

## Description<a name="check-staffing-description"></a>
+ Checks the current working queue, or queue you specify in the block, for whether agents are [available](real-time-metrics-definitions.md#available-real-time), [staffed](real-time-metrics-definitions.md#staffed-real-time), or [online](real-time-metrics-definitions.md#online-real-time)\.
+ Before transferring a call to agent and putting that call in a queue, use the **Check hours of operation** and **Check staffing** blocks\. They verify that the call is within working hours and that agents are staffed to service\.

## Supported channels<a name="check-staffing-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Contact flow types<a name="check-staffing-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="check-staffing-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-staffing-properties.png)

In the **Status to check** dropdown box, choose one of the following options:
+ [Available](real-time-metrics-definitions.md#available-real-time) = Check whether the agent has **Available** slots to be routed a contact\.
+ [Staffed](real-time-metrics-definitions.md#staffed-real-time) = Check whether agents have **Available** slots, or are **On call**, or are in **After Contact Work**\.
+ [Online](real-time-metrics-definitions.md#online-real-time) = Check whether agents are **Available**, in the **Staffed** state, or in a custom state\.

## Configuration tips<a name="check-staffing-tips"></a>
+ You must set a queue before using a **Check staffing** block in your contact flow\. You can use a [Set working queue](set-working-queue.md) block to set the queue\.
+ If a queue is not set, the contact is routed down the **Error** branch\.
+ When a contact is transferred from one flow to another, the queue that is set in a contact flow is passed from that flow to the next flow\.

## Configured block<a name="check-staffing-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-staffing-configured.png)

## Scenarios<a name="check-staffing-scenarios"></a>

See these topics for scenarios that use this block:
+ [Transfer contacts to a specific agent](transfer-to-agent.md)