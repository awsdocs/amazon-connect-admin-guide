# Investigate issues/call drivers detected in Contact Lens<a name="contact-lens-issue-detection"></a>

As a call center manager, you may have hundreds of calls to review so you can identify issues\. Contact Lens makes this process much faster by highlighting potential issues \(also known as call drivers\) that need further investigation\. You can quickly scan the transcript to identify issues or what the call is about, instead of listening to the entire audio of the conversation, or reading the entire transcript\. 

The following image shows an example of how Contact Lens highlights the primary call driver or reason for the customer outreach in the call transcript\. You can use this information to identify common emerging patterns across customer conversations\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-issue-in-transcript.png)

Unlike the categorization of contacts, you don't need to configure issue detection to use this feature\. Issues are detected by a machine learning model, based on an analysis of each turn in the conversation\.

## How to review transcripts for issues/call drivers<a name="how-to-review-transcript-for-issues"></a>

1. Go to the transcript\.

1. Scan for the highlighted text\.

1. Choose the timestamp for the highlighted turn\. Amazon Connect automatically takes you to that part of the audio\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-click-audio-timestamp.png)

1. Listen to the issue\.

**Tip**  
Issues are highlighted only in conversations that occur after the release of the issue detection feature on June 30, 2020\. 