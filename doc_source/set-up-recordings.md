# Set Up Recording Behavior<a name="set-up-recordings"></a>

Managers can monitor live conversations, and review and download recordings of past agent conversations\. To set this up, you need to add the **Set recording behavior** block to your contact flows, assign managers the appropriate permissions, and show them how to monitor live conversations and access past recordings in Amazon Connect\.

A conversation is recorded only when the contact is connected to an agent\. The contact is not recorded before then, when they are connected to the flow\. 

**Tip**  
When a customer is on hold, the agent is still recorded\.

Agents and contacts are stored on separate, stereo audio channels\.
+ The agent audio is stored in the right channel\. 
+ All incoming audio, including the customer and anyone conferenced in, is stored in the left channel\. 

Recordings are stored in the Amazon S3 bucket that you [specify for your instance](update-instance-settings.md)\. This allows access by any user or application with the appropriate permissions\. Encryption is enabled by default for all call recordings using Amazon S3 server\-side encryption with KMS\. You shouldn't disable encryption\.

**Important**  
For voice conversations to be stored in an Amazon S3 bucket, you need to enable recording in the contact flow block using the **Set recording behavior** block\.
For chat conversations, if there's an S3 bucket for storing chat transcripts, then all chats are recorded and stored there\. If no bucket exists, then no chats are recorded\. However, if you want to monitor chat conversations, you still need to add the **Set recording behavior** block to the flow\.

To view a sample contact flow with the **Set recording behavior** block configured, see [Sample Recording Behavior](sample-recording-behavior.md)\.

**To set up recording behavior in your contact flows**

1. Log in to your Amazon Connect instance using an account that has permissions to edit contact flows\.

1. Choose **Routing**, **Contact flows**, and then open the contact flow that handles customer contacts you want to monitor\. 

1. Before the contact is connected to an agent, add a **Set recording behavior** block to the contact flow\.

1. To configure the block to monitor chat conversations, you need to choose **Agent and Customer**\.

   If you're configuring the block for voice conversations only, you can choose **Agent and Customer**, **Agent only**, or **Customer only**\.

1. Choose **Save** and then **Publish** to publish the updated contact flow\.

**To set up recording behavior for outbound calls**

1. Create a contact flow, using the outbound whisper flow type\.

1. Add **Set recording behavior** to that contact flow\.

1. Set up a queue that will be used for making outbound calls\. In the **Outbound whisper flow** box, choose the contact flow that has **Set recording behavior** in it\. 

To learn what permissions managers need, and how they can monitor live conversations and review recordings of past conversations, see [Monitor Live Conversations](monitor-conversations.md) and [Review Recorded Conversations](review-recorded-conversations.md)\.

## When Are Recordings Available?<a name="when-are-recordings-available"></a>

When call recording is enabled, the recording is placed in your S3 bucket shortly after the contact is disconnected\. Then you can [review the recording](review-recorded-conversations.md)\.

**Important**  
You can also access the recording from the customer's [contact trace record \(CTR\)](sample-ctr.md)\. The recording is available in the CTR, however, only after the contact has left the [After Contact Work \(ACW\) state](metrics-agent-status.md#agent-status-acw)\. 