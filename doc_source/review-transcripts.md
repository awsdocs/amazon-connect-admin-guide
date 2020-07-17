# Review analyzed conversations using Contact Lens<a name="review-transcripts"></a>

By using Contact Lens for Amazon Connect, you can review the transcript and identify what part of the call is of interest\. You won't need to listen to an entire call to find out what's interesting about it\. 

For example, you might see that 25 seconds into the call the customer moved from a negative sentiment to a positive one\. You can download the recording and fast\-forward 25 seconds to listen to that portion of the call\.

## Review an analysis of a voice conversation<a name="review-analysis-of-voice-conversation"></a>

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Contact search** and **Contact Lens \- speech analytics** permissions\.

1. In Amazon Connect, choose **Metrics and quality**, **Contact search**\.

1. Use the filters on the page to narrow your search for a contact\. For date, you can search up to 14 days at a time\. For more information about searching for contacts, see [Contact search](contact-search.md)\. 

1. Choose the contact ID to view the Contact Trace Record \(CTR\) for the contact\.

1. In the **Recording and transcript** section of the CTR, review what was spoken and when, and their sentiment\.

1. If desired, choose the play prompt to listen to the recording\. Or, download the recording and fast\-forward to only the portion you're interested in\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-hit.png)

## Why don't I see color\-coded bars on my Amazon Connect console?<a name="where-are-color-coded-bars"></a>

If your Amazon Connect console doesn't include color\-coded bars similar to those shown in the preceding image, check whether the conversation that you're trying to analyzed occurred before June 30, 2020\. 

This view of conversations works only if the Contact Lens is enabled, and then the conversation occurred after June 30, 2020\. This is because the feature that displays analyzed conversations in this format was released on June 30, 2020, and it can only be applied to conversations that happen after that time\. 