# Enable Contact Lens for Amazon Connect<a name="enable-analytics"></a>


|  | 
| --- |
| Contact Lens for Amazon Connect is in preview release and is subject to change\. | 

When you enable Contact Lens, it produces a transcript of a call recording\. It analyzes the transcript and gives you sentiment scores\. You can search the transcript for keywords and sentiment scores to quickly identify which calls to investigate\. 

Contact Lens must be enabled in two places:
+ Your existing Amazon Connect instance\. By default, Contact Lens is enabled in new instances of Amazon Connect\.
+ Any contact flow that you want to analyze\.

The transcript that Amazon Connect generates is stored in the same Amazon S3 bucket as call recordings\. It's also encrypted with the same key\.

For an existing instance, to enable Contact Lens, you need to make sure an Amazon S3 bucket is specified for call recordings\. This is where the transcripts will be stored as well\. For instructions, see [Update Instance Settings](update-instance-settings.md)\. 

**To enable Contact Lens in a contact flow**

1. Add the **Set recording and analytics behavior** block to a contact flow\.

1. In the contact block, under **Call recording**, choose **On**, **Agent and customer**\.

   You need both agent and customer call recordings to use Content Lens\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

1. Select **Enable analytics**\. If you don't see this option, Contact Lens for Amazon Connect hasn't been enabled for your instance\. To enable it, see [Update Instance Settings](update-instance-settings.md)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior2.png)

1. Choose the language\.

1. Choose **Save**\.