# Create a New Contact Flow<a name="create-contact-flow"></a>

The starting point for creating all contact flows is the contact flow designer\. It's a drag\-and\-drop work surface that enables you to link together blocks of actions\. For example, when a customer first enters your contact center, you can ask for some input and then play a prompt such as "Thank you\."

For descriptions of the available action blocks, see [Contact Block Definitions](contact-blocks.md)\.

## <a name="w11aac13c21b7b7"></a>

## Choose a Contact Flow Template<a name="template"></a>

Amazon Connect includes a set of nine contact flow templates\. Each template is for a specific scenario\. For example, the template for transferring to a queue contains only the appropriate contact blocks for that type of flow\. 

When you create a contact flow, you need to choose the right template for your scenario\. The following contact flow templates are available\. 


| Template | When to use | 
| --- | --- | 
|  **Customer queue flow**  |  Use to manage what the customer experiences while in queue, before being joined to an agent\. Customer queue flows are interruptible and can include actions such as an audio clip apologizing for a delay and offering an option to receive a callback, leveraging the **Transfer to queue** block\.  | 
|  **Customer hold flow**  |  Use to manage what the customer experiences while the customer is on hold\. With this flow, one or more audio prompts can be played to a customer using the **Loop prompts** block while waiting on hold\.  | 
|  **Customer whisper flow**  |  Use to manage what the customer experiences as part of an inbound call immediately before being joined with an agent\. The agent and customer whispers are played to completion, then the two are joined\.  | 
|  **Outbound whisper flow**  |  Use to manage what the customer experiences as part of an outbound call before being connected with an agent\. In this flow, the customer whisper is played to completion, then the two are joined\. For example, this flow can be used to enable call recordings for outbound calls with the **Set call recording behavior** block\.  | 
|  **Agent hold flow**  |  Use to manage what the agent experiences when on hold with a customer\. With this flow, one or more audio prompts can be played to an agent using the **Loop prompts** block while the customer is on hold\.  | 
| **Agent whisper flow** | Use to manage what the agent experiences as part of an inbound call immediately before being joined with a customer\. The agent and customer whispers are played to completion, then the two are joined\. | 
| **Transfer to agent flow** | Use to manage what the agent experiences when transferring to another agent\. This type of flow is associated with transfer to agent quick connects, and often plays messaging, then completes the transfer using the **Transfer to agent** block\. | 
| **Transfer to queue flow** | Use to manage what the agent experiences when transferring to another queue\. This type of flow is associated with transfer to queue quick connects, and often plays messaging, then completes the transfer using the **Transfer to queue** block\. | 

**To create a contact flow from a template**

1. In the navigation pane, choose **Routing**, **Contact flows**\.

1. Next to the **Create contact flow** button, choose the drop\-down arrow to see the list of templates\.

1. Type a name and a description for your contact flow\.

1. Search for a contact block using the **Search** bar, or expand the relevant group to locate the block\. For descriptions of the contact blocks, see [Contact Block Definitions](contact-blocks.md)\.

1. Drag and drop the contact flow blocks onto the canvas\. You can add blocks in any order or sequence, as connections between elements aren't required to be strictly linear\.

1. Double\-click the title of the block\. In the configuration pane, configure settings for that block\.

## Create a Contact Flow \(Inbound\)<a name="new"></a>

1. In the navigation pane, choose **Routing**, **Contact flows**\.

1. Choose **Create contact flow**\. This opens the contact flow designer\. 

1. Type a name and a description for your contact flow\.

1. Search for a contact block using the **Search** bar, or expand the relevant group to locate the block\. For descriptions of the contact blocks, see [Contact Block Definitions](contact-blocks.md)\.

1. Drag and drop contract blocks onto the canvas\. You can add blocks in any order or sequence, as connections between elements aren't required to be strictly linear\.

1. Double\-click the title of the block\. In the configuration pane, configure settings for that block and then choose **Save** to close the pane\.

1. Back on the canvas, click on the first \(the originating\) block\.

1. Choose the circle for the action to perform, such as ****Success\.

1. Drag the arrow to the connector of the group that performs the next action\. For groups that support multiple branches, drag the connector to the appropriate action\. 

1. Repeat the steps to create a contact flow that meets your requirements\.

1. Choose **Save** to save a draft of the flow\. Choose **Publish** to activate the flow immediately\.

**Note**  
All connectors must be connected to a block in order to successfully publish your contact flow\.

## Generate Logs<a name="logs"></a>

After your contact flow is published live, you can use contact flow logs to help analyze contact flows and quickly find errors your customers encounter\. If needed, you can roll back to a previous version of the contact flow\. 

For more information about enabling and using contact flow logs, see [Contact Flow Logs](contact-flow-logs.md)\. 

## Roll back a Contact Flow<a name="rollback"></a><a name="rollback"></a>

1. In the contact flow designer, open the contact flow you want to roll back\.

1. Use the drop\-down to choose the version of the contact flow you want to roll back to\. If you choose **Latest**, it reverts the flow to the most recent published version\. If there isn't a published version, it reverts to the most recent saved version\. 
**Note**  
To see a consolidated view of all changes across all flows, click the **View historical changes** link at the bottom of the Contact flows page\. You can filter to a specific flow by date or user name\.

1. Choose **Publish** to push that version into production\. 