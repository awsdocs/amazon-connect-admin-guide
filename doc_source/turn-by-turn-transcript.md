# Quickly navigate transcripts and audio<a name="turn-by-turn-transcript"></a>

Supervisors are often required to review many agents calls for quality assurance purposes\. The turn\-by\-turn transcript and sentiment data helps you quickly identify and navigate to the portion of the recording that is of interest to you\. 

The following image shows features that enable you to quickly navigate transcripts and audio to find areas that need your attention\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-navigate-transcripts2.png)

1. Use [Show transcript summary](#contact-lens-contact-summarization) to review only the issue, outcome, and/or action item\.

1. Use [Autoscroll](#autoscroll) to jump around the audio or transcript\. The two always stay in sync\.

1. Scan for [sentiment emojis](#sentiment-emojis) to quickly identify a part for the transcript you want to listen to\.

1. Choose the timestamp to jump to that part of the audio recording\.

## Show transcript summary<a name="contact-lens-contact-summarization"></a>

It can be time\-consuming to review contact transcripts that are hundreds of lines long\. To make this process faster and more efficient, Contact Lens provides the option for you to view a transcript summary\. The summary shows only those lines where Contact Lens has identified an issue, outcome, or action item in the transcript\. 
+ **Issue** represents the call driver\. For example, "I'm thinking of upgrading to your online subscription plan\." 
+ **Outcome** represent sthe likely conclusion or outcome of the contact\. For example, "Based on your current plan I would recommend the online essentials plans that we have\."
+ **Action item** represent sthe action item the agent takes\. For example, "Please keep an eye out for an email with a price quote\. I will send it to you shortly\."

Each contact has no more than one issue, one outcome, and one action item\. Not all contacts will have all three\. 

**Note**  
If Contact Lens displays the message **There is no summary information for this transcript**, it means no issue, outcome, or action item was identified\.

You don't need to configure call summarization\. It works out\-of\-the\-box without any training of the machine learning model\. 

## Turn on autoscroll to synchronize the transcript and audio<a name="autoscroll"></a>

Autoscroll enables you to jump around the audio or transcript, and the two always stay in sync\. For example:
+ When you listen to a conversation, the transcript moves along with it, showing you sentiment emojis and any detected issue\.
+ You can scroll through the transcript, and choose the timestamp for the turn to listen to that specific point in the recording\.

Because the audio and transcript are aligned, the transcript can help you understand what the agent and customer are saying\. This is especially useful when:
+ The audio is bad, maybe due to a connection issue\. The transcript can help you understand what's being said\.
+ There's a dialect or language variant\. Our models are trained on different accents so the transcript can help you understand what's being said\.

## Scan for sentiment emojis<a name="sentiment-emojis"></a>

Sentiment emojis help you quickly scan a transcript so you can listen to that part of the conversation\.

For example, where you see red emojis for customer turns and then a green emoji, you might choose the timestamp to jump to that specific point of the recording to hear how that agent helped the customer\.

## Tap or click category tags to navigate through transcript<a name="category-navigation"></a>

When you tap or click on the category tags, Contact Lens auto\-navigates to the corresponding point\-of\-interests in the transcript\. There are also category markers in the recording playback visualization to indicate which part of the audio file has utterances related to the category\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-tag-navigation.png)