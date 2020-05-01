# Contact Block: Set Disconnect Flow<a name="set-disconnect-flow"></a>

## In contact flow types<a name="set-disconnect-flow-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Description<a name="set-disconnect-flow-description"></a>
+ Specifies which contact flow to run after a disconnect event during chat conversation\. A disconnect event is when an agent disconnects\. When the disconnect event occurs, the corresponding content flow runs\. 
+ This block is only used in chat scenarios\. If a customer stops responding to the chat, use this block to decide whether to run the disconnect flow and call a [Wait](wait.md) block, or end the conversation\.

## Properties<a name="set-disconnect-flow-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow-properties.png)

## Configured block<a name="set-disconnect-flow-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow-configured.png)

## Sample flows<a name="set-disconnect-flow-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample Inbound Flow \(First Contact Experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-disconnect-flow-scenarios"></a>

See these topics for scenarios that use this block:
+ [Example Chat Scenario](chat.md#example-chat-scenario)