# Default Contact Flows<a name="contact-flow-default"></a>

Amazon Connect includes a set of default contact flows that have already been published\. It uses them to power your contact center\. 

For example, say you create a contact flow that includes putting the customer on hold, but you don't create a prompt for it\. The default contact flow, **Default agent hold**, will be played automatically\. This is a way to help you get started with your call center quickly\.

**Tip**  
If you want to change the behavior of a default contact flow, we recommend you instead just create a new customized default with a different name than the original\. Then call it intentionally in your contact flows rather than defaulting to it\. This will give you better control over how your contact flows work\.

To see the list of default flows in the Amazon Connect console, go to **Routing**, **Contact Flows**\. They all start with **Default** in their name\. 

Following is a description of each default flow\.

## Default Agent Hold<a name="default-agent-hold"></a>

The default agent hold flow is the experience the agent receives when placed on hold\. During this flow, a **Loop prompt** block plays the message “You are on hold” to the agent every 10 seconds\. 

## Default Agent Transfer<a name="default-agent-transfer"></a>

This default transfer flow is the customer's experience when the customer is transferred to an agent by using [Create Quick Connects](transfer.md#quick-connects)\. A **Play prompt** plays the message “Transferring now\.” Then the **Transfer to agent** block is used to transfer the contact to the agent\. 

**Tip**  
The **Transfer to Agent** block is a beta feature and only works for voice interactions\. To transfer a chat contact to another agent, follow these instructions: [Using Contact Attributes to Route Contacts to a Specific Agent](transfer.md#use-attribs-agent-queue)\.

## Default Customer Queue<a name="default-customer-queue"></a>

This default contact flow is played when a customer is placed in a queue\. The loop has a one\-time voice prompt and queue music in \.wav format that's been uploaded to the Amazon Connect instance\. 

The customer remains in this loop until their call is answered by an agent\.

## Default Customer Whisper<a name="default-customer-whisper"></a>

This contact flow starts immediately before the call is connected\. It uses a "beep" sound to notify a customer that their call has been connected to an agent\. 

## Default Agent Whisper<a name="default-agent-whisper"></a>

This contact flow plays for the agent immediately before the call is connected with the customer\. This type of flow can be used to play a prompt for the agent\. 

The name of the queue is played to the agent\. It identifies for the agent the queue that the customer was in\. The name of the queue is retrieved from the system variable `$.Queue.Name`\. 

For more information about system variables, see [Contact Flow System Attributes](connect-attrib-list.md#attribs-system-table)\.

## Default Customer Hold<a name="default-customer-hold"></a>

This contact flow starts when the customer is put on hold\. It plays the audio that the customer hears while on hold\. 

## Default Outbound<a name="default-outbound"></a>

This contact flow is an outbound whisper that manages what the customer experiences as part of an outbound call, before being connected with an agent\. 

It starts with an optional **Set recording behavior** block\. Then a prompt plays indicating the call isn't being recorded, and the flow ends\.

The customer remains in the system \(on the call\) after the flows ends\. 

## Default Queue Transfer<a name="default-queue-transfer"></a>

This contact flow is manages what the customer experiences when they are transferred to another queue\.

It starts with a **Check hours of operation** block to check the hours of operation for the current queue\. The **In hours** option branches to the **Check staffing** block to determine whether agents are available, staffed, or online\. 

If it returns **True** \(agents are available\), the flow goes to the **Transfer to queue** block\. If it returns **False** \(no agents are available\), the flow plays a prompt and disconnects the call\.