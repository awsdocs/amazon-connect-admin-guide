# Flow block: Transfer to agent \(beta\)<a name="transfer-to-agent-block"></a>

## Description<a name="transfer-to-agent-block-description"></a>
+ Ends the current flow and transfers the customer to an agent\. 
**Note**  
If the agent is already with someone else, the contact is disconnected\.  
If the agent is in After Contact Work, they are automatically removed from ACW at the time of transfer\.
+ The **Transfer to Agent** block is a beta feature and works only for voice interactions\.
+ We recommend using the [Set working queue](set-working-queue.md) block for agent\-to\-agent transfers instead of using this block\. The **Set working queue** block supports omnichannel transfers such as voice and chat\. For instructions, see [Set up agent\-to\-agent transfers](setup-agent-to-agent-transfers.md)\. 

## Supported channels<a name="transfer-to-agent-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

To transfer chats and tasks to agents, use the [Set working queue](set-working-queue.md) block\. Because [Set working queue](set-working-queue.md) works for all channels, we recommend using it for voice calls too, instead of using **Transfer to agents \(beta\)**\. For instructions, see [Set up agent\-to\-agent transfers](setup-agent-to-agent-transfers.md)\.

## Flow types<a name="transfer-to-agent-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="transfer-to-agent-block-properties"></a>

The following image shows the **Properties** page of the **Transfer to agent** block\. It does not have any options on it\.

![\[The properties page of the Transfer to agent block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-agent-properties.png)

## Configured block<a name="transfer-to-agent-block-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It displays the status **Transferred**\. It does not have any branches\. 

![\[A configured Transfer to agent block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-agent-configured.png)

## Scenarios<a name="transfer-to-agent-block-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up contact transfers](transfer.md)