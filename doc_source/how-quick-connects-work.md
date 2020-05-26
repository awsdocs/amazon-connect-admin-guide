# How Quick Connects Work<a name="how-quick-connects-work"></a>

This article explains how each type of quick connect works: agent, queue, and external quick connects\. It explains which contact flows are used, and what appears on the agent's Contact Control Panel \(CCP\)\.

**Tip**  
For all three types of quick connects, when the quick connect is invoked, the contact that the agent is working on hears the [Default customer hold](default-customer-hold.md) flow unless you specify a different customer hold flow\. 

## Agent Quick Connects<a name="agent-quick-connects"></a>

Let's say an agent named John is talking to a customer\. During the conversation he needs to transfer the call to an agent named Maria\. This is an agent quick connect\.

Here's what John and Maria do, and what contact blocks are triggered: 

1. John chooses the **Quick Connect** button on his CCP\. \(On the earlier CCP, the button is named **Transfer**\)\. He selects **Maria** from the list of quick connects\. 

   When John does this, his CCP banner changes to **Connected**\. However, the call isn't actually connected to Maria yet\. 

1. In our example scenario, Amazon Connect triggers an agent transfer flow that looks like the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-flow-transfer-agent-transfer-flow.png)

   The call is not yet connected to Maria\.

1. John hears the first **Play prompt**, "Transferring to agent\."

1. Maria receives a notification in her CCP to either accept or reject the call\.

1. Maria accepts the incoming call\. The banner in her CCP changes to **Connecting**\.

1. The first [Set Whisper Flow](set-whisper-flow.md) block is triggered\. This block sets the custom agent whisper flow\. It plays the Custom\_Agent\_Whisper to Maria, for example, "This is an internal call transferred from another agent\."
**Note**  
If you don't create and then select a custom agent whisper flow, Amazon Connect plays the [default agent whisper flow](default-agent-whisper.md), which says the queue name\. 

1. The next [Set Whisper Flow](set-whisper-flow.md) block is triggered\. It plays the Custom\_Customer\_Whisper to John, for example, "Your call is not connecting to an agent\." 
**Note**  
If you don't create and then select a custom customer whisper flow, Amazon Connect plays the [default customer whisper flow](default-customer-whisper.md), which plays a beep\. 

1. Maria's CCP banner shows she's **Connected**\. John and Maria are connected and can start talking\.

1. Now John can do one of the following on his CCP:
   + Choose **Join**\. This joins all parties on the call\. John, Maria, and the customer have a conference call\.
   + Choose **Hold all**\. This puts Maria and the customer on hold\.
   + Put Maria on hold, so he only talks to the customer\.
   + Choose **End call**\. He leaves the call but Maria and the customer are directly connected and continue talking\.

## Queue Quick Connects<a name="queue-quick-connects"></a>

Let’s say John is talking to a customer\. The customer needs help resetting his password, so John needs to transfer him to the PasswordReset queue\. This is a queue quick connect\.

Another agent, Maria, is assigned to handle contacts in the PasswordReset queue\. Her status in the CCP is **Available**\. 

Here's what John and Maria do, and what contact blocks are triggered:

1. John chooses the **Quick Connect** button on his CCP\. \(On the earlier CCP, the button is named **Transfer**\)\. He chooses to transfer the contact to the PasswordReset queue\. As soon as John chooses the PasswordReset quick connect, his CCP banner shows **Connecting**\. 
**Important**  
Even though the status of the transferred call \(internal\-transfer\) shows on John's CCP banner as **Connecting**, the contact is not yet transferred to the PasswordReset queue\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-flow-transfer-transfer-connecting.png)

1. Amazon Connect invokes the queue transfer flow that's associated with the PasswordReset quick connect\. In this flow, the [Transfer to Queue](transfer-to-queue.md) block transfers the contact to the PasswordReset queue since it's specified in the block\. The contact is now in the PasswordReset queue\.

1. Maria is notified in her CCP to accept or reject the incoming call\. 

1. Maria accepts the incoming call and her CCP banner changes to **Connecting**\.

1. The [Agent whisper flow](create-contact-flow.md#contact-flow-types) is played to Maria\. It says "Connecting you to PasswordReset queue\."

1. The [Customer whisper flow](create-contact-flow.md#contact-flow-types) is played to John\. It says "Connecting you to PasswordReset queue\."

1. Maria's CCP banner changes to **Connected**\. John and Maria are connected and can start talking\. 

1. Now John can do one of the following from his CCP:
   + Choose **Join**\. This joins all parties on the call\. John, Maria, and the customer have a conference call\.
   + Choose **Hold all**\. This puts Maria and the customer on hold\.
   + Put Maria on hold, so he only talks to the customer\.
   + Choose **End call**\. He leaves the call but Maria and the customer are directly connected and continue talking\.

## External Quick Connects<a name="external-quick-connects"></a>

There are no contact flows involved in external quick connect\. When an agent invokes an external quick connect, the call is directly connected the destination without invoking any flows\.

Because no contact flow is involved in external quick connects, you can't set the outbound caller ID\. Instead, the caller ID that you specified when you [created the queue](create-queue.md) is used\. 