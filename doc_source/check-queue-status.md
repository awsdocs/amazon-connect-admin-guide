# Flow block: Check queue status<a name="check-queue-status"></a>

## Description<a name="check-queue-status-description"></a>
+ Checks the status of the queue based on specified conditions\.
+ Branches based on the comparison of **Time in Queue** or **Queue capacity**\. 
  + **Time in queue** is the amount of time the oldest contact spends in queue, before they are routed to an agent or removed from the queue\.
  + **Queue capacity** is number of contacts waiting in a queue\.
+ If no match is found, the **No Match** branch is followed\.

## Supported channels<a name="check-queue-status-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="check-queue-status-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="check-queue-status-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-queue-status-properties.png)

## Configuration tips<a name="check-queue-status-tips"></a>

The order in which you add conditions matters at the runtime\. Results are evaluated against conditions in the same order in which you add them to the block\. Contacts are routed down the first condition to match\. 

For example, in the following condition order, every value matches one of first two conditions\. None of the other conditions are ever matched\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-queue-status-example1.png)

In this next example, all contacts with a wait time in queue of 90 or less \(<=90\) match first condition only\. This means less than or equal to 9 \(<=9\), <=12, <=15, <=18, <=20, <=21 are never run\. Any value greater than 90 is routed down the greater than or equal to 21 \(>=21\) condition branch\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-queue-status-example2.png)

## Configured block<a name="check-queue-status-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-queue-status-configured.png)

## Scenarios<a name="check-queue-status-scenarios"></a>

See these topics for scenarios that use this block:
+ [Manage contacts in a queue](queue-to-queue-transfer.md)