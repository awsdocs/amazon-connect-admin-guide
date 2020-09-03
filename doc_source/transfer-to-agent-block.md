# Contact block: Transfer to agent \(beta\)<a name="transfer-to-agent-block"></a>

## Contact flow types<a name="transfer-to-agent-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="transfer-to-agent-block-description"></a>
+ Ends the current contact flow and transfers the customer to an agent\. If the agent is already with someone else, the contact is disconnected\.
+ The **Transfer to Agent** block is a beta feature and works only for voice interactions\.
+ We recommend using the [Set working queue](set-working-queue.md) block for agent\-to\-agent transfers instead of using this block\. The **Set working queue** block supports omnichannel transfers such as voice and chat\. For instructions, see [Set up agent\-to\-agent transfers](setup-agent-to-agent-transfers.md)\. 

## Properties<a name="transfer-to-agent-block-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-agent-properties.png)

## Configured block<a name="transfer-to-agent-block-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-agent-configured.png)

## Scenarios<a name="transfer-to-agent-block-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up contact transfers](transfer.md)