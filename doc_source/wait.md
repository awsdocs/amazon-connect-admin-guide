# Contact block: Wait<a name="wait"></a>

## Contact flow types<a name="wait-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow

## Description<a name="wait-description"></a>
+ Use this block in chat contact flows only\. If a contact stops responding to a chat, this block pauses the contact flow for the specified wait time\. 
+ If this block is triggered during a voice conversation, the contact is routed down the **Error** branch\.

## Properties<a name="wait-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wait-properties.png)

It has two properties: 
+ **Timeout**: Run this branch if the customer hasn't sent a message after a specified amount of time\. Maximum is 24 hours\.
+ **Customer return**: Run this branch when the customer returns and sends a message\. With this branch you can route the customer to the previous \(same\) agent, previous \(same\) queue, or override and set a new working queue or agent\. 

## Configuration tips<a name="wait-tips"></a>

You can add multiple **Wait** blocks to your contact flows\. For example: 
+ If the customer comes back in 5 minutes, connect them to the same agent\. This is because that agent has all of the context\.
+ If the customer doesn't come back after 5 minutes, send a text saying "We missed you\." 
+ If the customer comes back in 12 hours, connect to a contact flow that puts them in a priority queue\. However, it doesn't route them to the same agent\.

## Configured block<a name="wait-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wait-configured.png)

## Sample flows<a name="wait-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample disconnect flow](sample-disconnect.md)

## Scenarios<a name="wait-scenarios"></a>

See these topics for scenarios that use this block:
+ [Example chat scenario](chat.md#example-chat-scenario)