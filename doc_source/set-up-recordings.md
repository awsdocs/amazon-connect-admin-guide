# Set Up Recording Behavior<a name="set-up-recordings"></a>

Managers can review and download recordings of past agent conversations\. To set this up, you need to add the **Set recording behavior** block to your contact flows, assign managers the appropriate permissions, and show them how to access the recordings in Amazon Connect\.

A conversation is recorded only when the contact is connected to an agent\. The contact is not recorded before then, when they are connected to the flow\. 

Agents and contacts are stored on separate, stereo audio channels\.
+ The agent audio is stored in the right channel\. 
+ All incoming audio, including the customer and anyone conferenced in, is stored in the left channel\. 

Recordings are stored in the Amazon S3 bucket that you [specify for your instance](update-instance-settings.md)\. This allows access by any user or application with the appropriate permissions\. Encryption is enabled by default for all call recordings using Amazon S3 server\-side encryption with KMS\. You shouldn't disable encryption\.

**Important**  
For voice conversations, you enable recording in the contact flow block, and you can specify whether to record the agent, customer, or both\. For chat conversations, you enable recording at the instance level\. If there's an S3 bucket for storing chat transcripts, then all chats are recorded\. If no bucket exists, then no chats are recorded\.

**To set up recording behavior in your contact flows**

1. Log in to your Amazon Connect instance using an account that has permissions to edit contact flows\.

1. Choose **Routing**, **Contact flows**, and then open the contact flow that handles customer contacts you want to monitor\. 

1. Before the contact is connected to an agent, add a **Set recording behavior** block to the contact flow\. In the block, choose **Agent and Customer**, and then choose **Save**\.
**Important**  
Make sure that the block has connections to the block before and after it in the contact flow\.

1. Open **Set recording behavior** to configure it\. Choose what you want to record: Agent, Chat bot, Customer, or all of them\. 

1. To enable manager monitoring and recording for outbound calls, the contact flow in which you add **Set recording behavior** must be in the flow selected as the outbound contact flow for the queue used for outbound calls\.

1. Choose **Save and Publish** to publish the updated contact flow\. Choose **Save and Publish** again to confirm that you want to overwrite the published version\.

**To set up recording behavior for outbound calls**

1. Create a contact flow, using the outbound whisper flow type\.

1. Add **Set recording behavior** to that contact flow\.

1. Set up a queue that will be used for making outbound calls\. In the **Outlook whisper flow** box, choose the contact flow that has **Set recording behavior** in it\. 

To learn what permissions managers need so they can monitor live conversations and review recordings of past conversations, see [Review Recorded Conversations](recordings.md)\.