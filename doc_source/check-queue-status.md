# Contact block: Check queue status<a name="check-queue-status"></a>

## Description<a name="check-queue-status-description"></a>
+ Checks the status of the queue based on specified conditions\.
+ Branches based on the comparison of **Time in Queue** or **Queue capacity**\. 
  + **Time in queue** is the amount of time the oldest contact spends in queue, before they are routed to an agent or removed from the queue\.
  + **Queue capacity** is number of contacts waiting in a queue\.
+ If no match is found, the **No Match** branch is followed\.

## Contact flow types<a name="check-queue-status-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="check-queue-status-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-queue-status-properties.png)

## Configured block<a name="check-queue-status-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-queue-status-configured.png)

## Scenarios<a name="check-queue-status-scenarios"></a>

See these topics for scenarios that use this block:
+ [Manage contacts in a queue](queue-to-queue-transfer.md)