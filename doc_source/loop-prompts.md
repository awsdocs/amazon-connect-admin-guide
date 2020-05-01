# Contact Block: Loop Prompts<a name="loop-prompts"></a>

## In contact flow types<a name="loop-prompts-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Customer Queue flow
+ Customer Hold flow
+ Agent Hold flow

## Description<a name="loop-prompts-description"></a>
+ Loops a sequence of prompts while a customer or agent is on hold or in queue\.

## Properties<a name="loop-prompts-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/loop-prompts-properties.png)

## Configuration tips<a name="loop-prompts-tips"></a>
+ When **Loop prompts** is used in a Queue flow, audio playback can be interrupted with a flow at preset times\.
+ Always use an interruption period that's greater than 20 seconds\. This is the amount of time an available agent has to accept the contact\. If the interruption period is less than 20 seconds, you might get contacts going down the **Error** branch\. This is because Amazon Connect doesn't support dequeueing the customer when they are being routed to an active agent and are in the 20 second window to join\.
+ The internal counter for the loop is persisted for the call, not the contact flow\. If you reuse the contact flow during a call, the loop counter isn't reset\.
+ If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\. 
+ Some existing contact flows have a version of the **Loop prompts** block that doesn't have an **Error** branch\. In this case, a chat contact stops execution of the customer queue flow\. The chat is routed when the next agent becomes available\.

## Configured block<a name="loop-prompts-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/loop-prompts-configured.png)

## Sample flows<a name="loop-prompts-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample Interruptible Queue Flow with Callback](sample-interruptible-queue.md)

## Scenarios<a name="loop-prompts-scenarios"></a>

See these topics for scenarios that use this block:
+ [Manage Contacts in a Queue](queue-to-queue-transfer.md)