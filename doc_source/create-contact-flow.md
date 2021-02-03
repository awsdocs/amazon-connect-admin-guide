# Create a new contact flow<a name="create-contact-flow"></a>

The starting point for creating all contact flows is the contact flow designer\. It's a drag\-and\-drop work surface that enables you to link together blocks of actions\. For example, when a customer first enters your contact center, you can ask for some input and then play a prompt such as "Thank you\."

For descriptions of the available action blocks, see [Contact block definitions](contact-block-definitions.md)\.

## Before you begin: develop a naming convention<a name="before-create-contact-flow"></a>

Chances are you're going to create tens or hundreds of contact flows\. To help you stay organized, it's important to develop a naming convention\. Once you start creating contact flows, we strongly recommend against renaming them\.

**You can't delete a contact flow**\. To get obsolete contact flows out of your way, we recommend appending **zzTrash\_** to their name\. This will also make them easy to find should you want to reuse them in the future\.

## Choose a contact flow type<a name="contact-flow-types"></a>

Amazon Connect includes a set of nine contact flow types\. **Each type has only those blocks for a specific scenario\.** For example, the contact flow type for transferring to a queue contains only the appropriate contact blocks for that type of flow\. 

**Important**  
When you create a contact flow, you need to choose the right type for your scenario\. Otherwise, the blocks you need may not be available\. 
You can't import flows of different types\. This means if you start with one type and need to switch to another to get the right blocks, you have to start over\.

The following contact flow types are available\. 


| Type | When to use | 
| --- | --- | 
|  **Inbound contact flow**  |  This is the generic contact flow type that's created when you choose the **Create contact flow** button, and don't select a type using the drop\-down arrow\. It creates an inbound contact flow\.  This contact flow works with voice, chat, and tasks\.   | 
|  **Customer queue flow**  |  Use to manage what the customer experiences while in queue, before being joined to an agent\. Customer queue flows are interruptible and can include actions such as an audio clip apologizing for a delay and offering an option to receive a callback, leveraging the **Transfer to queue** block\. This contact flow works with voice, chat, and tasks\.   | 
|  **Customer hold flow**  |  Use to manage what the customer experiences while the customer is on hold\. With this flow, one or more audio prompts can be played to a customer using the **Loop prompts** block while waiting on hold\. This contact flow works with voice\.   | 
|  **Customer whisper flow**  |  Use to manage what the customer experiences as part of an inbound call immediately before being joined with an agent\. The agent and customer whispers are played to completion, then the two are joined\. This contact flow works with voice and chat\.   | 
|  **Outbound whisper flow**  |  Use to manage what the customer experiences as part of an outbound call before being connected with an agent\. In this flow, the customer whisper is played to completion, then the two are joined\. For example, this flow can be used to enable call recordings for outbound calls with the **Set recording behavior** block\. This contact flow works with voice and chat\.   | 
|  **Agent hold flow**  |  Use to manage what the agent experiences when on hold with a customer\. With this flow, one or more audio prompts can be played to an agent using the **Loop prompts** block while the customer is on hold\. This contact flow works with voice\.   | 
| **Agent whisper flow** | Use to manage what the agent experiences as part of an inbound call immediately before being joined with a customer\. The agent and customer whispers are played to completion, then the two are joined\. This contact flow works with voice, chat, and tasks\.   | 
| **Transfer to agent flow** | Use to manage what the agent experiences when transferring to another agent\. This type of flow is associated with transfer to agent quick connects, and often plays messaging, then completes the transfer using the **Transfer to agent** block\. This contact flow works with voice, chat, and tasks\.   | 
| **Transfer to queue flow** | Use to manage what the agent experiences when transferring to another queue\. This type of flow is associated with transfer to queue quick connects, and often plays messaging, then completes the transfer using the **Transfer to queue** block\. This contact flow works with voice, chat, and tasks\.  | 

## Create an inbound contact flow<a name="create-inbound-contact-flow"></a>

Use these steps to create an inbound contact flow\. 

1. In the navigation pane, choose **Routing**, **Contact flows**\.

1. Choose **Create contact flow**\. This opens the contact flow designer and creates an inbound contact flow \(Type = Contact flow\)\. 

1. Type a name and a description for your contact flow\.

1. Search for a contact block using the **Search** bar, or expand the relevant group to locate the block\. For descriptions of the contact blocks, see [Contact block definitions](contact-block-definitions.md)\.

1. Drag and drop contract blocks onto the canvas\. You can add blocks in any order or sequence, as connections between elements aren't required to be strictly linear\.
**Tip**  
You can move blocks around the canvas so the layout aligns to your preferences\. To select multiple blocks at the same time, press the **Ctrl** key on your laptop \(or the **Cmd** key on a Mac\), choose the blocks you want, and then use your mouse to drag them as a group within the contact flow\. You can also use the **Ctrl**/**Cmd** key to start at one point on the canvas and drag your pointer across the canvas to select all blocks included in the frame\. 

1. Double\-click the title of the block\. In the configuration pane, configure settings for that block and then choose **Save** to close the pane\.

1. Back on the canvas, click on the first \(the originating\) block\.

1. Choose the circle for the action to perform, such as ****Success\.

1. Drag the arrow to the connector of the group that performs the next action\. For groups that support multiple branches, drag the connector to the appropriate action\. 

1. Repeat the steps to create a contact flow that meets your requirements\.

1. Choose **Save** to save a draft of the flow\. Choose **Publish** to activate the flow immediately\.

**Note**  
All connectors must be connected to a block in order to successfully publish your contact flow\.

## Generate logs<a name="logs"></a>

After your contact flow is published live, you can use contact flow logs to help analyze contact flows and quickly find errors your customers encounter\. If needed, you can roll back to a previous version of the contact flow\. 

For more information about using contact flow logs, see [Track events as customers interact with contact flows](about-contact-flow-logs.md)\. 