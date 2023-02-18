# Set up recording behavior<a name="set-up-recordings"></a>

Managers can monitor live conversations, and review and download recordings of past agent conversations\. To set this up, you need to add the [Set recording and analytics behavior](set-recording-behavior.md) block to your flows, assign managers the appropriate permissions, and show them how to monitor live conversations and access past recordings in Amazon Connect\.

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
For voice conversations to be stored in an Amazon S3 bucket, you need to enable recording in the flow block using the [Set recording and analytics behavior](set-recording-behavior.md) block\.
For chat conversations, if there's an S3 bucket for storing chat transcripts, then all chats are recorded and stored there\. If no bucket exists, then no chats are recorded\. However, if you want to monitor chat conversations, you still need to add the [Set recording and analytics behavior](set-recording-behavior.md) block to the flow\.

**Tip**  
We recommend using the contact ID to search for recordings\.  
Even though many call recordings for specific contact IDs may be named with the contact ID prefix itself \(for example, 123456\-aaaa\-bbbb\-3223\-2323234\.wav\), there is no guarantee that the contact IDs and name of the contact recording file *always* match\. By using **Contact ID** for your search on the [Contact search](search-recordings.md) page, you can find the correct recording by referring the audio file on the contact record\.

## When are recordings available?<a name="when-are-recordings-available"></a>

When call recording is enabled, the recording is placed in your S3 bucket shortly after the contact is disconnected\. Then you can [review the recording](review-recorded-conversations.md)\.

**Important**  
You can also access the recording from the customer's [contact record](sample-ctr.md)\. The recording is available in the contact record, however, only after the contact has left the [After Contact Work \(ACW\) state](metrics-agent-status.md#agent-status-acw)\. 

**Tip**  
Amazon Connect uses the Amazon S3 [PutObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_PutObject.html) and [MultipartUpload](https://docs.aws.amazon.com/AmazonS3/latest/API/API_MultipartUpload.html) APIs to upload the call recording to your S3 bucket\. If you are using [S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) when call recordings are uploaded successfully to your bucket, make sure you enable the notification for **All object create events**, or for both *s3:ObjectCreated:Put* and *s3:ObjectCreated:CompleteMultipartUpload* event types\. 

## How to set up recording behavior<a name="how-to-set-up-recording-behavior"></a>

To view a sample flow with the **Set recording behavior** block configured, see [Sample recording behavior](sample-recording-behavior.md)\.

**To set up recording behavior in your flows**

1. Log in to your Amazon Connect instance using an account that has permissions to edit flows\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/menu-contact-flows.png)

1. Open the flow that handles customer contacts you want to monitor\.

1. In the flow, before the contact is connected to an agent, add a [Set recording and analytics behavior](set-recording-behavior.md) block to the contact flow\.

1. To configure the [Set recording and analytics behavior](set-recording-behavior.md) block, choose from the following: 
   + To record voice conversations, choose what you want to record: **Agent and Customer**, **Agent only**, or **Customer only**\.
   + To record chat conversations, you need to choose **Agent and Customer**\.
   + To enable monitoring of voice and/or chat conversations, you need to choose **Agent and Customer**\.

1. Choose **Save** and then **Publish** to publish the updated flow\.

**To set up recording behavior for outbound calls**

1. Create a flow, using the outbound whisper flow type\.

1. Add a [Set recording and analytics behavior](set-recording-behavior.md) block to that contact flow\.

1. Set up a queue that will be used for making outbound calls\. In the **Outbound whisper flow** box, choose the flow that has [Set recording and analytics behavior](set-recording-behavior.md) in it\. 

## How to set up users to monitor conversations or review recordings<a name="overview-setup-managers-review-recordings"></a>

To learn what permissions managers need, and how they can monitor live conversations and review recordings of past conversations, see:
+ [Set up live monitoring for voice and/or chat](monitor-conversations.md) 
+ [Review recorded conversations](review-recorded-conversations.md)

## How to set up S3 Object Lock for immutable call recordings<a name="s3-object-lock-call-recordings"></a>

You can use Amazon S3 Object Lock in combination with your call recording bucket to help prevent call recordings from being deleted or overwritten for a fixed amount of time, or indefinitely\. 

Object Lock adds another layer of protection against object changes and deletion\. It can also help meet regulatory requirements for Write\-Once\-Read\-Many \(WORM\) storage\.

### Important things to know<a name="s3-object-lock-important"></a>
+ You can enable Amazon S3 Object Lock only on new buckets\. To configure it on an existing call recording bucket, contact AWS Support\.
+ Versioning must be enabled on your call recording bucket\.
+ After Amazon S3 Object Lock is enabled it cannot be removed\.
+ We recommend using a dedicated call recording bucket because all objects will be locked after the default Object Lock retention policy is applied\.
+ Ensure that your retention policy is appropriate for your requirements\. After the policy is configured, your call recordings will be protected from deletion for the duration specified\.
+ We highly recommended you thoroughly test the policy in a non\-production environment before implementing it in production\.

### Step 1: Create a new S3 bucket with Object Lock enabled<a name="configure-s3-object-lock-step1"></a>

For a tutorial on creating a new S3 bucket with Object Lock enabled, see [Protect Data on Amazon S3 Against Accidental Deletion or Application Bugs Using S3 Versioning, S3 Object Lock, and S3 Replication](http://aws.amazon.com/getting-started/hands-on/protect-data-on-amazon-s3/)\. 

To enable Object Lock on an existing bucket, open an AWS Support ticket\.

### Step 2: Configure Amazon Connect to use the new S3 bucket for call recordings<a name="configure-s3-object-lock-step2"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Data storage**\.

1. In the **Call recordings** section, choose **Edit**\.

1. Choose **Select an existing S3 bucket**, and then in the **Name** dropdown box choose the new Object Lock bucket\.

1. Choose **Save**\.

### Step 3: Test Object Lock is enabled<a name="configure-s3-object-lock-step3"></a>

1. Make a test call to your contact center to generate a call recording\.

1. Log in to Amazon Connect at https://*your\-instance*\.my\.connect\.aws/home, with an Admin account, or an account that has [permissions to search for contacts](contact-search.md#required-permissions-search-contacts)\. 

1. Choose **Analytics and optimization**, **Contact search**\. Search for your call recording to find the contact ID\. Copy the contact ID\. You're going to use it in the next step to locate the call recording in your S3 bucket\.

1. Open the Amazon S3 console, select the bucket you created in Step 1, and follow the path prefix\. The path to the call recording includes the year, month, and day the recording was made\. After you're in the correct path prefix, search for the contact ID of the call recording\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/s3-objectlock-pathprefix.png)

1. Select the **Show versions** toggle next to the **Search** box\. This option allows you to attempt to delete the object instead of only applying a delete marker\. Applying a delete marker is the standard behavior when you delete an object from an S3 bucket with versioning enabled\.

1. Select the call recording \(the box to the left of the recording name\), and then choose **Delete**\. In the confirmation box, type **permanently delete** and select **Delete objects**\.

1. Review the **Delete objects: status** notification to confirm that the delete operation has been blocked due to the Object Lock policy\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/s3-objectlock-failed.png)