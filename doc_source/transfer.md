# Set Up Call Transfers<a name="transfer"></a>

To make it easy for you to transfer contacts, Amazon Connect provides you with several tools: 
+ Two contact flow types:
  + Transfer to agent: Enables transfers to another agent\.
  + Transfer to queue: Enables transfers to a queue\.
+ Action blocks:
  + **Transfer to queue**: Use to end the current contact flow and place the customer in a queue\. 
  + **Transfer to phone number**: Use to transfer the customer to a phone number, such as an external number\.
  + **Transfer to flow**: Use to end the current flow and transfer the customer to another contact flow\.
+ Quick connects: Use to create common destinations for transfers\. Agents will see them as options in the CCP when they go to do a transfer\.

This topic explains how to create quick connects and use transfer contact blocks in specific scenarios\. 

## Overview of Steps<a name="transfer-overview"></a>

**To set up call transfers and quick connects**

1. Choose a contact flow type based on what you want to do: Transfer to agent or Transfer to queue\. External transfers do not require a specific type of contact flow\.

1. Create and publish the contact flow\. 

1. Create a quick connect for the type of transfer to enable: **Agent**, **Queue**, or **External**\.

   When you create the **Agent** or **Queue** quick connect, select a contact flow that matches the type of transfer to enable\. **External** quick connects require only a phone number, and do not allow you to set a queue or contact flow\.

1. Add the quick connect that you created to any queue used in a contact flow for which to enable call transfer, such as the queue used in the contact flow for incoming calls\. Make sure the queue is in a routing profile assigned to the agents who transfers calls\. 

## Create Quick Connects<a name="quick-connects"></a>

Quick connects are a way for you to create a list of destinations for common transfers\. For example, you might create a quick connect for Tier 2 support\. If agents in Tier 1 support can't solve the issue, they will transfer the contact to Tier 2\. 

When you create a quick connect, you can specify one of these destinations: 
+ **External**—Contacts are transferred to an external number \(such as an on\-call pager\)\. 
+ **Agent**—Contacts are transferred to a specific agent as part of a contact flow\.
+ **Queue**—Contacts are transferred to a queue as part of a contact flow\.
**Important**  
Agent and Queue quick connects only appear in the CCP when an agent transfers a call\. 

**To create a quick connect**

1. Choose **Routing**, **Quick connects**, **Add a new destination**\.

1. Enter a name for the connect\. Choose the type, and then specify the destination \(such as a phone number or the name of an agent\), contact flow \(if applicable\), and description\.
**Important**  
A description is required when you create a quick connect\. If you don't add one, you'll get an error when you try to save the quick connect\. 

1. To add more quick connects, choose **Add new **\.

1. Choose **Save**\.

**To enable your agents to see the quick connects in the CCP when they transfer a contact**

1. After you create the quick connect, go to **Routing**, **Queues** and then choose the appropriate queue for the contact to be routed to\.

1. On the Edit queue page, in the Quick connect box, search for the quick connect you created\.

1. Select the quick connect and then choose **Save**\.

## Resume a Contact Flow After Transfer<a name="contact-flow-resume"></a>

Let's say you need to transfer a contact to an external department that's not using Amazon Connect\. For example, maybe you need to transfer the caller to a shipping provider to check the status of their delivery\. After the contact is disconnected from the external number, you want them to be returned to your agent, for example, when the delivery company couldn't resolve their issue\. 
+ For advanced automation, send tracking information as DTMF digits when the call is transferred, so that the shipment information is retrieved with the transferred call before the customer is connected\.

**To set up a contact flow for this scenario**

1. Add a **Transfer to phone number** block to your contact flow\.

1. In the **Transfer to phone number** block, enter the following settings:
   + **Transfer to**
     + **Phone number**—Sets the phone number to transfer the call to\.
     + **Use attribute**—Specify a contact attribute to set the phone number to transfer the call to\.
   + **Set timeout**
     + **Timeout \(in seconds\)**—The number of seconds to wait for the recipient to answer the transferred call\.
   + **Use attribute**—Specify a contact attribute to use to set the **Timeout** duration\.
   + **Resume contact flow after disconnect**—When you select this option, after the call is transferred, the caller is returned to the contact flow when the call with the third party ends\. Additional branches for **Success**, **Call failed**, and **Timeout** are added to the block when you select this option so that you can appropriately route contacts when there is an issue with the transfer\.
   + **Optional parameters**
     + **Send DTMF**—Select **Send DTMF** to include up to 50 Dual\-Tone Multi\-frequency \(DTMF\) characters with the transferred call\. You can enter the characters to include, or use an attribute\. Use the DTMF characters to navigate an automated IVR system that answers the call\.
     + **Caller ID number**—Specify the caller ID number used for transferred call\. You can select a number from your instance, or use an attribute to set the number\.
     + **Caller ID name**—Specify the caller ID name used for the transferred call\. You can enter a name, or use an attribute to set the name\.

       In some cases, the caller ID information is provided by the carrier of the party you are calling\. The information may not be up\-to\-date with that carrier, or the number may get passed differently between systems because of hardware or configuration differences\. If that is the case, the person you call may not see the phone number, or may see the name of a previously registered owner of the number, instead of the name you specify in the block\.

1. Connect **Transfer to phone number** to the rest of your contact flow\.

When the block executes: 

1. The call is transferred to the external number\.

1. Optionally, when the conversation with the external party ends, the contact is returned to the contact flow\.

1. The contact then follows the **Success** branch from the block to continue the flow\.

1. If the call is not successfully transferred, one of the other branches is followed: **Call failed**, **Timeout**, or **Error**, depending on the reason the caller did not return to the flow\.

## Manage Calls in a Queue Using a Transfer to Queue Block<a name="queue-to-queue-transfer"></a>

For calls coming into your contact center, you can define advanced routing decisions to minimize queue wait times, or route calls to specific queues, using blocks in your contact flow\. For example, use a **Check queue status** block to check staffing or agent availability for a queue before sending a call to that queue, or use a **Get queue metrics** block to retrieve queue metrics\. Then use a **Check contact attributes** block to check specific queue metric attributes, and define conditions in the block to determine which queue to route the call to based on attribute values\. For more information about using queue metrics, see [How to Use System Metric Attributes](attrib-system-metrics.md)\.

After determining which queue to transfer the call to, use a **Transfer to queue** block in a contact flow to transfer the call to that queue\. When the **Transfer to queue** block runs, it checks the queue capacity to determine whether or not the queue is at capacity \(full\)\. This check for queue capacity compares the current number of calls in the queue to the **Maximum contacts in queue** limit, if one is set for the queue\. If no limit is set, the queue is limited to the number of concurrent active calls set in the service limit for the instance\.

After the call is placed in a queue, the call remains there until an agent takes the call, or until the call is handled based on the routing decisions in your customer queue flow\. To change the queue associated with the call after it is already placed in a queue, use a **Loop prompts** block with a **Transfer to queue** block in a customer queue flow\. In the block choose which queue to transfer the call to, or use an attribute to set the queue\.

In the **Transfer to queue** block, there are two outputs to route calls through: the **Success** branch or the **At capacity** branch\. When a call is successfully transferred to a queue and follows the **Success** branch, the call remains associated with the current customer queue flow after being transferred\. When the call is not successfully transferred to a queue and follows the **At capacity** branch because the queue is at capacity, the call remains in the current working queue\.

**To manage calls in a queue using a Transfer to queue block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Choose the down arrow next to **Create contact flow**, then choose **Create customer queue flow**\.

1. Under **Interact**, add a **Loop prompts** block to provide a message to the caller when the call is transferred, then every X seconds or minutes while the call is in the queue\.

1. Select the **Loop prompts** block to display the settings for the block\.

1. Choose **Add another prompt to the loop**\.

1. Under **Prompts**, do one of the following:
   + Choose **Audio recording** in the drop\-down menu, then select the audio recording to use as the prompt\.
   + Choose **Text to Speech** in the drop\-down menu, then enter text to use for the prompt in the **Enter text to be spoken** field\.

1. To set an interrupt, choose **Interrupt every**, enter a value for the interrupt interval, and then choose a unit, either **Minutes** or **Seconds**\. We recommend that you use an interval greater than 20 seconds to ensure that queued contacts that are being connected to an agent are not interrupted\.

1. Choose **Save**\.

1. Connect the block to the **Entry point** block in the contact flow\.

1. Under **Terminate/Transfer**, drag a **Transfer to queue** block onto the designer\.

1. Select the title of the block to display the settings for the block, then choose the **Transfer to queue** tab\.

1. Under **Queue to check**, choose **Select a queue**, then select the queue to transfer calls to\.

   Alternatively, choose **Use attribute**, then reference an attribute to specify the queue\. If you use an attribute to set the queue, the value must be the queue ARN\.

1. Choose **Save**\.

1. Connect the **Loop prompt** block to the **Transfer to queue** block\.

1. Add additional blocks to complete the contact flow that you require, such as the blocks to check queue status or metrics, then choose **Save**\.

   The contact flow is not active until you publish it\.

**Important**  
To successfully complete the call transfer to another queue, you must include a block after the **Transfer to queue** block and connect the **Success** branch to it\. For example, use an **End flow / Resume** block to end the contact flow\. The flow does not end until the call is picked up by an agent\.

## Transfer Calls Directly to a Specific Agent<a name="transfer-to-agent"></a>

With agent queues, you can route calls directly to a specific agent\. This can allow you to provide a consistent customer experience for your customers by letting you route calls directly to the agent the customer last interacted with if that agent is available\. In each block that supports transferring the contact to a queue, such as the **Transfer to queue** block, there is a **By agent** radio button under **Queue** \(or **Queue to check \(optional\)** or **By queue** depending on the block\)\. When you select **By agent**, a drop\-down list that includes all of the users in your instance is displayed\. When you select a user name, the contact is transferred to the queue for that user\.

Contact flow blocks in which you can specify a queue include: **Set working queue**, **Get queue metrics**, **Check queue status**, **Check staffing**, and **Transfer to queue** when used in a customer queue flow\.

**Note**  
A queue is created for all users in your Amazon Connect instance, but only users assigned permissions to use the Contact Control Panel \(CCP\) can use the CCP to receive calls\. The Agent and Admin security profiles are the only default security profiles that include permissions to use the CCP\. If you route a call to a user that cannot access the CCP, the contact can never be answered\.

**To route a call directly to a specific agent**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. In the contact flow designer, open an existing contact flow, or create a new one\.

1. Add a block in which you can select a queue to transfer a contact to, such as a **Set working queue** block\.

1. Select the title of the block to open the block settings\.

1. Select **By agent**\.

1. Under **Select an agent**, enter the user name of the agent, or select the agent's user name from the drop\-down list\.

1. Choose **Save**\.

1. Connect the **Success** branch to the next block in your contact flow\.

You can also choose to use an attribute to select the queue created for the agent user account\. To do so, after you choose **By agent**, choose **Use attribute**\.

### Using Contact Attributes to Route Contacts to a Specific Agent<a name="use-attribs-agent-queue"></a>

When you use contact attributes in a contact flow to route calls to an agent, the attribute value must be either the agent's user name, or the agent's user ID\.

To determine the user ID for an agent so that you can use the value as an attribute, use the [ListUsers](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListUsers.html) operation to retrieve the users from your instance\. The agent's user ID is returned with the results from the operation as the value of the `Id` in the [UserSummary](https://docs.aws.amazon.com/connect/latest/APIReference/API_UserSummary.html) object\.

You can also find the user ID for an agent by using [Amazon Connect Agent Event Streams](agent-event-streams.md)\. The agent events, which are included in the agent event data stream, include the agent ARN\. The user ID is included in the agent ARN after `agent/`\. In the following example, agent event data, the agent ID is **87654321\-4321\-4321\-4321\-123456789012**\.

```
{
    "AWSAccountId": "123456789012",
    "AgentARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent/87654321-4321-4321-4321-123456789012",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent-state/76543210-7654-6543-8765-765432109876",
            "Name": "Available",
            "StartTimestamp": "2019-01-02T19:16:11.011Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "IAM",
            "LastName": "IAM",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/routing-profile/aaaaaaaa-bbbb-cccc-dddd-111111111111",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/aaaaaaaa-bbbb-cccc-dddd-222222222222",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [{
                    "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/aaaaaaaa-bbbb-cccc-dddd-222222222222",
                    "Name": "BasicQueue"
                }],
                "Name": "Basic Routing Profile"
            },
            "Username": "agentUserName"
        },
        "Contacts": []
},
```