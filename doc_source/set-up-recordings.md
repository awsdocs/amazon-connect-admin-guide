# Set up recording behavior<a name="set-up-recordings"></a>

Managers can monitor live conversations, and review and download recordings of past agent conversations\. To set this up, you need to add the [Set recording and analytics behavior ](set-recording-behavior.md) block to your contact flows, assign managers the appropriate permissions, and show them how to monitor live conversations and access past recordings in Amazon Connect\.

## When is a conversation recorded?<a name="when-conversation-recorded"></a>

A conversation is recorded only when the contact is connected to an agent\. The contact is not recorded before then, when they are connected to the flow\.

When a customer is on hold, the agent is still recorded\.

If the agent mutes their own microphone, for example, to consult with a coworker sitting next to them, their side\-bar conversation is not recorded\. The customer is still recorded since their microphone hasn't been muted\.

## Where are recordings and transcripts stored?<a name="where-are-recordings-stored"></a>

Agents and contacts are stored on separate, stereo audio channels\.
+ The agent audio is stored in the right channel\. 
+ All incoming audio, including the customer and anyone conferenced in, is stored in the left channel\. 

Recordings are stored in the Amazon S3 bucket that are [created for your instance](amazon-connect-instances.md#get-started-data-storage)\. Any user or application with the appropriate permissions can access the recordings in the Amazon S3 bucket\. 

Encryption is enabled by default for all call recordings using Amazon S3 server\-side encryption with KMS\. The encryption is at the object level\. The reports and recording objects are encrypted; there's no encryption at the bucket level\.

You shouldn't disable encryption\.

**Important**  
For voice conversations to be stored in an Amazon S3 bucket, you need to enable recording in the contact flow block using the [Set recording and analytics behavior ](set-recording-behavior.md) block\.
For chat conversations, if there's an S3 bucket for storing chat transcripts, then all chats are recorded and stored there\. If no bucket exists, then no chats are recorded\. However, if you want to monitor chat conversations, you still need to add the [Set recording and analytics behavior ](set-recording-behavior.md) block to the flow\.

## When are recordings available?<a name="when-are-recordings-available"></a>

When call recording is enabled, the recording is placed in your S3 bucket shortly after the contact is disconnected\. Then you can [review the recording](review-recorded-conversations.md)\.

**Important**  
You can also access the recording from the customer's [contact trace record \(CTR\)](sample-ctr.md)\. The recording is available in the CTR, however, only after the contact has left the [After Contact Work \(ACW\) state](metrics-agent-status.md#agent-status-acw)\. 

## How to set up recording behavior<a name="how-to-set-up-recording-behavior"></a>

To view a sample contact flow with the **Set recording behavior** block configured, see [Sample recording behavior](sample-recording-behavior.md)\.

**To set up recording behavior in your contact flows**

1. Log in to your Amazon Connect instance using an account that has permissions to edit contact flows\.

1. Choose **Routing**, **Contact flows**, and then open the contact flow that handles customer contacts you want to monitor\. 

1. Before the contact is connected to an agent, add a [Set recording and analytics behavior ](set-recording-behavior.md) block to the contact flow\.

1. To configure the [Set recording and analytics behavior ](set-recording-behavior.md) block, choose from the following: 
   + To record voice conversations, choose what you want to record: **Agent and Customer**, **Agent only**, or **Customer only**\.
   + To record chat conversations, you need to choose **Agent and Customer**\.
   + To enable monitoring of voice and/or chat conversations, you need to choose **Agent and Customer**\.

1. Choose **Save** and then **Publish** to publish the updated contact flow\.

**To set up recording behavior for outbound calls**

1. Create a contact flow, using the outbound whisper flow type\.

1. Add a [Set recording and analytics behavior ](set-recording-behavior.md) block to that contact flow\.

1. Set up a queue that will be used for making outbound calls\. In the **Outbound whisper flow** box, choose the contact flow that has [Set recording and analytics behavior ](set-recording-behavior.md) in it\. 

## How to set up users to monitor conversations or review recordings<a name="overview-setup-managers-review-recordings"></a>

To learn what permissions managers need, and how they can monitor live conversations and review recordings of past conversations, see:
+ [Monitor live conversations](monitor-conversations.md) 
+ [Review recorded conversations](review-recorded-conversations.md)