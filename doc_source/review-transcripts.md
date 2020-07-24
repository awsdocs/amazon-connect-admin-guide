# Review analyzed conversations using Contact Lens<a name="review-transcripts"></a>

By using Contact Lens for Amazon Connect, you can review the transcript and identify what part of the call is of interest\. You won't need to listen to an entire call to find out what's interesting about it\. 

For example, you might scan the transcript of the call and see a red sentiment emoji for a customer turn\. You can choose the timestamp and jump to that portion of audio recording\.

## Review an analysis of a voice conversation<a name="review-analysis-of-voice-conversation"></a>

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Contact search** and **Contact Lens \- speech analytics** permissions\.

1. In Amazon Connect, choose **Metrics and quality**, **Contact search**\.

1. Use the filters on the page to narrow your search for a contact\. For date, you can search up to 14 days at a time\. For more information about searching for contacts, see [Contact search](contact-search.md)\. 

1. Choose the contact ID to view the Contact Trace Record \(CTR\) for the contact\.

1. In the **Recording and transcript** section of the CTR, review what was spoken and when, and their sentiment\.

1. If desired, choose the play prompt to listen to the recording\. Or, download the recording and fast\-forward to only the portion you're interested in\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-hit.png)

## Turn\-by\-turn transcript<a name="turn-by-turn-transcript"></a>

Busy supervisors often need to review a lot of calls\. The turn\-by\-turn transcript and sentiment data helps you quickly identify and navigate to the portion of the recording that is of interest to you\. 

Following are key features of the turn\-by\-turn transcript:

**Auto scroll**  
The audio recording and transcript are in sync\. You can quickly scroll through the transcript, stop at interesting turns, and choose the timestamp for the turn to listen that specific point in the recording\. 

**Sentiment emojis**  
For example, where you see red emojis for customer turns and then a green emoji, you might choose the timestamp to jump to that specific point of the recording to hear how that agent helped the customer\.

**Issue detection**  
Issues \(also known as call drivers\) are turns where primary call driver or reason for the customer outreach is underlined in the transcript\. You can use this information to identify common emerging patterns across customer conversations\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-navigate-transcripts.png)

## Why don't I see color\-coded bars on my Amazon Connect console?<a name="where-are-color-coded-bars"></a>

If your Amazon Connect console doesn't include color\-coded bars similar to those shown in the preceding image, check whether the conversation that you're trying to analyzed occurred before June 30, 2020\. 

This view of conversations works only if the Contact Lens is enabled, and then the conversation occurred after June 30, 2020\. This is because the feature that displays analyzed conversations in this format was released on June 30, 2020, and it can only be applied to conversations that happen after that time\. 