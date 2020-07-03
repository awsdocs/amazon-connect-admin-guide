# Enable Contact Lens for Amazon Connect<a name="enable-analytics"></a>


|  | 
| --- |
| Contact Lens for Amazon Connect is in preview release and is subject to change\. | 

When you enable Contact Lens, it produces a transcript of a call recording\. It analyzes the transcript and gives you sentiment scores\. You can search the transcript for keywords and sentiment scores to quickly identify which calls to investigate\. 

The transcript that Amazon Connect generates is stored in the same Amazon S3 bucket as call recordings\. It's also encrypted with the same key\.

Contact Lens must be enabled in two places:

1. Your existing Amazon Connect instance\. By default, Contact Lens is enabled in new instances of Amazon Connect\.

1. Any contact flow that you want to analyze\.

## How to enable Contact Lens in an instance<a name="enable-analytics-instance"></a>

For an existing instance, to enable Contact Lens, you need to make sure an Amazon S3 bucket is specified for call recordings\. This is where the transcripts will be stored as well\. For instructions, see [Update instance settings](update-instance-settings.md)\. 

## How to enable Contact Lens in a contact flow<a name="enable-analytics-contact-flow"></a>

To enable Contact Lens in a contact flow, you add a [Set Recording Behavior](set-recording-behavior.md) block to the flow, and configure it for Contact Lens\.

**Tip**  
If you want to transfer a contact to another agent or queue, and you want to continue using Contact Lens to collect data, you need to add to the flow another [Set Recording Behavior](set-recording-behavior.md) block with **Enable analytics** turn on\. This is because a transfer generates a second contact ID and CTR\. Contact Lens needs to run on that CTR as well\. 

**To enable Contact Lens in a contact flow**

1. Add the [Set Recording Behavior](set-recording-behavior.md) block to a contact flow\.

1. In the contact block, under **Call recording**, choose **On**, **Agent and customer**\.

   You need both agent and customer call recordings to use Content Lens\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

1. Select **Enable analytics**\. If you don't see this option, Contact Lens for Amazon Connect hasn't been enabled for your instance\. To enable it, see [Update instance settings](update-instance-settings.md)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior2.png)

1. Choose the language\.

1. Choose **Save**\.

1. If the contact is going to be transferred to another agent or queue, repeat these steps to add another [Set Recording Behavior](set-recording-behavior.md) block with **Enable analytics** turned on\.