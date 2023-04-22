# Create a new flow<a name="create-contact-flow"></a>

The starting point for creating all flows is the flow designer\. It's a drag\-and\-drop work surface that enables you to link together blocks of actions\. For example, when a customer first enters your contact center, you can ask for some input and then play a prompt such as "Thank you\."

For descriptions of the available action blocks, see [Flow block definitions](contact-block-definitions.md)\.

## Before you begin: develop a naming convention<a name="before-create-contact-flow"></a>

Chances are you're going to create tens or hundreds of flows\. To help you stay organized, it's important to develop a naming convention\. After you start creating flows, we strongly recommend against renaming them\.

## Choose a flow type<a name="contact-flow-types"></a>

Amazon Connect includes a set of nine flow types\. **Each type has only those blocks for a specific scenario\.** For example, the flow type for transferring to a queue contains only the appropriate flow blocks for that type of flow\. 

**Important**  
When you create a flow, you need to choose the right type for your scenario\. Otherwise, the blocks you need may not be available\. 
You can't import flows of different types\. This means if you start with one type and need to switch to another to get the right blocks, you have to start over\.

The following flow types are available\. 


| Type | When to use | 
| --- | --- | 
|  **Inbound flow**  |  This is the generic flow type that's created when you choose the **Create flow** button, and don't select a type using the drop\-down arrow\. It creates an inbound flow\.  This flow works with voice, chat, and tasks\.   | 
|  **Customer queue flow**  |  Use to manage what the customer experiences while in queue, before being joined to an agent\. Customer queue flows are interruptible and can include actions such as an audio clip apologizing for a delay and offering an option to receive a callback, leveraging the **Transfer to queue** block\. This flow works with voice, chat, and tasks\.   | 
|  **Customer hold flow**  |  Use to manage what the customer experiences while the customer is on hold\. With this flow, one or more audio prompts can be played to a customer using the **Loop prompts** block while waiting on hold\. This flow works with voice\.   | 
|  **Customer whisper flow**  |  Use to manage what the customer experiences as part of an inbound call immediately before being joined with an agent\. The agent and customer whispers are played to completion, then the two are joined\. This contact flow works with voice and chat\.   | 
|  **Outbound whisper flow**  |  Use to manage what the customer experiences as part of an outbound call before being connected with an agent\. In this flow, the customer whisper is played to completion, then the two are joined\. For example, this flow can be used to enable call recordings for outbound calls with the **Set recording behavior** block\. This contact flow works with voice and chat\.   | 
|  **Agent hold flow**  |  Use to manage what the agent experiences when on hold with a customer\. With this flow, one or more audio prompts can be played to an agent using the **Loop prompts** block while the customer is on hold\. This flow works with voice\.   | 
| **Agent whisper flow** | Use to manage what the agent experiences as part of an inbound call immediately before being joined with a customer\. The agent and customer whispers are played to completion, then the two are joined\. This contact flow works with voice, chat, and tasks\.   | 
| **Transfer to agent flow** | Use to manage what the agent experiences when transferring to another agent\. This type of flow is associated with transfer to agent quick connects, and often plays messaging, then completes the transfer using the **Transfer to agent** block\. This flow works with voice, chat, and tasks\.   Do not place any sensitive information in this flow\. When a cold transfer occurs, the transferring agent disconnects before transfer is completed, and this flow is run on the caller\. This means information in the flow is played to the caller, not the agent\.    | 
| **Transfer to queue flow** | Use to manage what the agent experiences when transferring to another queue\. This type of flow is associated with transfer to queue quick connects, and often plays messaging, then completes the transfer using the **Transfer to queue** block\. This flow works with voice, chat, and tasks\.  | 

## Create an inbound flow<a name="create-inbound-contact-flow"></a>

Use these steps to create an inbound flow\. 

1. In the left navigation menu, choose **Routing**, **Contact flows**\.   
![\[The Amazon Connect navigation menu.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/menu-contact-flows.png)

1. Choose **Create flow**\. This opens the flow designer and creates an inbound flow \(Type = Flow\)\. 

1. Type a name and a description for your flow\.

1. Search for a flow block using the **Search** bar, or expand the relevant group to locate the block\. For descriptions of the contact blocks, see [Flow block definitions](contact-block-definitions.md)\.

1. Drag and drop contract blocks onto the canvas\. You can add blocks in any order or sequence, as connections between elements aren't required to be strictly linear\.
**Tip**  
You can move blocks around the canvas so the layout aligns to your preferences\. To select multiple blocks at the same time, press the **Ctrl** key on your laptop \(or the **Cmd** key on a Mac\), choose the blocks you want, and then use your mouse to drag them as a group within the flow\. You can also use the **Ctrl**/**Cmd** key to start at one point on the canvas and drag your pointer across the canvas to select all blocks included in the frame\. 

1. Double\-click the title of the block\. In the configuration pane, configure settings for that block and then choose **Save** to close the pane\.

1. Back on the canvas, click on the first \(the originating\) block\.

1. Choose the circle for the action to perform, such as ****Success\.

1. Drag the arrow to the connector of the group that performs the next action\. For groups that support multiple branches, drag the connector to the appropriate action\. 

1. Repeat the steps to create a flow that meets your requirements\.

1. Choose **Save** to save a draft of the flow\. Choose **Publish** to activate the flow immediately\.

**Note**  
All connectors must be connected to a block in order to successfully publish your flow\.

## Delete flows<a name="delete-contact-flow"></a>

To delete flows use the [DeleteContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_DeleteContactFlow.html) API\. 

Currently, there's no way to delete flows using the Amazon Connect admin console\.

## Generate logs<a name="logs"></a>

After your flow is published live, you can use flow logs to help analyze flows and quickly find errors your customers encounter\. If needed, you can roll back to a previous version of the flow\. 

For more information about using flow logs, see [Track events as customers interact with flows](about-contact-flow-logs.md)\. 