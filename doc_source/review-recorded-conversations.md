# Review Recorded Conversations<a name="review-recorded-conversations"></a>

Managers can review past conversations between agents and customers\. To set this up, you need to [set up recording behavior](set-up-recordings.md), assign managers the appropriate permissions, and then show them how to access the recorded conversations\. 

**When is a conversation recorded?** A conversation is recorded only when the contact is connected to an agent\. The contact is not recorded before then, when they are connected to the IVR\. If the call is transferred externally, the call recording stops when the agent drops from the call\.

**Tip**  
When call recording is enabled, the recording is placed in your S3 bucket shortly after the contact is disconnected\. Then the recording is available for you to review it using the steps in this article\.   
You can also access the recording from the customer's [contact trace record \(CTR\)](sample-ctr.md)\. The recording is available in the CTR, however, only after the contact has left the [After Contact Work \(ACW\) state](metrics-agent-status.md#agent-status-acw)\.

## Review Recordings/Transcripts of Past Conversations<a name="review-recordings-and-transcripts"></a>

These are the steps that a manager does to review past recordings/transcripts of conversations\.

1. Log in to Amazon Connect with a user account that has [permissions to access recordings](assign-permssions-to-review-recordings.md)\.

1. In Amazon Connect choose **Metrics and quality**, **Contact search**\. 

1. Filter the list of contacts by date, agent login, phone number, or other criteria\. Choose **Search**\.

1. Conversations that were recorded have icons in the **Recording/Transcript** column\. If you don't have the appropriate permissions, you won't see these icons\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/recording-icons.png)

1. To listen to a recording of a voice conversation, or read the transcript of a chat, choose the **Play** icon\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-recordings.png)

1. The following image shows a sample chat transcript\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-chat-transcript.png)