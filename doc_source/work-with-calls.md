# Accept and Transfer Calls<a name="work-with-calls"></a>

When agents use the Contact Control Panel \(CCP\), they can perform the following actions on a softphone\. When they opt for a desk phone, they have the same controls as softphone\. The only difference is that there is no **Accept** button on a desk phone\.

## Accept Incoming Calls<a name="accept-calls"></a>
+ To accept an incoming call, choose **Accept call**\.
+ To edit settings, choose **Settings**\.
+ To end a call, choose **End call**\.
+ To put a call on hold, choose **Hold**\.

When a call is connected, a new set of options become available in the CCP\.

## Transfer Calls<a name="transfers"></a>

After an agent picks up a call, they can transfer the call by choosing the **Transfer** button and then choosing one of the available contacts\. To define this list of available contacts, you set up quick connects\. The quick connects are displayed in the list of contacts when an agent tries to transfer an active call\. 

Agents can also manually enter a phone number to transfer calls to by choosing **Dial number** after answering the call\. The agent can enter a phone number using the keypad, and then choose **Transfer** to transfer the call\. If agents regularly transfer calls to a specific external phone number, you can create an **External** contact flow and use that phone number for the destination\.

**To set up call transfers and quick connects**

1. Create and publish a contact flow for the type of transfer to enable\.
   + To enable transfers to another agent, create a Transfer to agent contact flow\.
   + To enable transfers to a queue, create a Transfer to queue contact flow\.
   + External transfers do not require a specific type of contact flow\.
**Note**  
You must publish your contact flows to make them active in your contact center\.

1. Create a quick connect for the type of transfer to enable: **Agent**, **Queue**, or **External**\.

   When you create the **Agent** or **Queue** quick connect, select a contact flow that matches the type of transfer to enable\. **External** quick connects require only a phone number, and do not allow you to set a queue or contact flow\.

   For more information about quick connects, see [Create Quick Connects](connect-contact-flows.md#quick-connects)\.

1. Add the quick connect that you created to any queue used in a contact flow for which to enable call transfer, such as the queue used in the contact flow for incoming calls\. The queue must be in the routing profile assigned to the agent who should be able to transfer calls\. 

**To transfer calls to an agent or queue**

1. After accepting a call in the CCP, choose **Transfer**\.

1. Select the contact to whom to transfer the call, and then choose **Dial**\.

   The call is placed on hold during the transfer\.

1. After the call is answered by an agent, or sent to a queue, choose **Leave call** to disconnect from the call\.

1. To use conference, swap, or hold:
+ To begin a conference call, choose **Join** to perform a soft transfer\. To drop out of the call, choose **Leave**\.
+ Choose **Swap** to switch between talking to a customer and the person to whom you’re transferring the call\.
+ Choose **Hold all** to put all parties on hold\.

Some settings that are configured in Amazon Connect include setting agents to go into the `After call work` state after they are done with their call\. Agents can also be configured to accept a call automatically, without having to choose **Accept**\.