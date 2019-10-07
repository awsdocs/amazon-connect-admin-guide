# Set Up Call Recording<a name="set-up-recordings"></a>

Managers can review and download recordings of past agent conversations\. To set this up, you need to add the **Set call recording behavior** block to your contact flows, assign managers the appropriate permissions, and show them how to access the recordings in Amazon Connect\. 

A conversation is recorded only when the contact is connected to an agent\. The contact is not recorded before then, when they are connected to the IVR\. 

**To set up call recording in your contact flows**

1. Log in to your Amazon Connect instance using an account that has permissions to edit contact flows\.

1. Choose **Routing**, **Contact flows**, and then open the contact flow that handles customer contacts you want to monitor\. 

1. Before the call is connected to an agent, add a **Set call recording behavior** block to the contact flow\. In the block, choose **Agent and Customer**, and then choose **Save**\.
**Important**  
Make sure that the block has connections to the block before and after it in the contact flow\.

1. To enable manager monitoring and recording for outbound calls, the contact flow in which you add **Set call recording behavior** must be in the flow selected as the outbound contact flow for the queue used for outbound calls\.

1. Choose **Save and Publish** to publish the updated contact flow\. Choose **Save and Publish** again to confirm that you want to overwrite the published version\.

To learn what permissions managers need so they can monitor live conversations and review recordings of past conversations, see [Review Recorded Conversations](recordings.md)\.