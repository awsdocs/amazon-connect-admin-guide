# Set up agent\-to\-agent transfers<a name="setup-agent-to-agent-transfers"></a>

We recommend using these instructions to set up agent\-to\-agent voice, chat, and task transfers\. You use a [Set working queue](set-working-queue.md) block to transfer the contact to the agent's queue\. The **Set working queue **block supports an omnichannel experience, whereas the [Transfer to agent \(beta\)](transfer-to-agent-block.md) block does not\.

## Step 1: Create the quick connect<a name="step1-create-quick-connect"></a>

 Following are the instructions to add quick connects manually using the Amazon Connect console\. To add quick connects programmatically, use the [CreateQuickConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateQuickConnect.html) API\.

**Create a quick connect**

1. On the navigation menu, choose **Routing**, **Quick connects**, **Add a new destination**\.

1. Enter a name for the connect\. Choose the type, and then specify the destination \(such as a phone number or the name of an agent\), flow \(if applicable\), and description\.
**Important**  
A description is required when you create a quick connect\. If you don't add one, you'll get an error when you try to save the quick connect\. 

1. To add more quick connects, choose **Add new**\.

1. Choose **Save**\.

1. Go to the next procedure to enable your agents to see the quick connects in the Contact Control Panel \(CCP\)\.

**Enable your agents to see the quick connects in the CCP when they transfer a contact**

1. After you create the quick connect, go to **Routing**, **Queues** and then choose the appropriate queue for the contact to be routed to\.

1. On the **Edit queue** page, in the **Quick connect** box, search for the quick connect you created\.

1. Select the quick connect and then choose **Save**\.

**Tip**  
Agents see all of the quick connects for the queues in their routing profile\.

## Step 2: Set up the "Transfer to agent" flow<a name="setup-agent-voice-transfers"></a>

In this step, you create a flow that's type **Transfer to agent** and use a [Set working queue](set-working-queue.md) block to transfer the contact to the agent\. 

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Use the drop\-down to choose **Create transfer to agent flow**\. 

1. Type a name and a description for your flow\.

1. In the left navigation menu, expand **Set**, and then drag the **Set working queue** block to the canvas\.

1. Configure the **Set working queue** block as shown in the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-working-queue-properties-agent-to-agent-transfer.png)

   1. Choose **By agent**\.

   1. Choose **Set dynamically**\.

   1. For **Namespace**, use the dropdown box to select **Agent**\.

   1. For **Value**, use the dropdown box to select **User name**\.

1. Add a [Transfer to queue](transfer-to-queue.md) block\. You don't need to configure this block\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-to-agent-transfer.png)

1. Save and publish this flow\.

1. To show your agents how to transfer chats to another agent, see [Transfer chats to another queue](transfer-chats.md)\. 

   To show your agents how to transfer tasks to another agent, see [Transfer a task](transfer-task.md)\. 