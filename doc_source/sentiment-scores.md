# Investigate sentiment scores in Contact Lens<a name="sentiment-scores"></a>

## What are sentiment scores?<a name="sentiment-scores"></a>

A sentiment score is an analysis of text, and a rating of whether it includes mostly positive, negative, or neutral language\. Supervisors can use sentiment scores to search conversations and identify calls that are associated with varying degrees of customer experiences, positive or negative\. It helps them identify which of their calls to investigate\. 

You can view a sentiment score for the entire conversation, as well as scores for each quarter of the call\.

## How to investigate sentiment scores<a name="how-to-use-sentiment-scores"></a>

When working to improve your contact center, you may want to focus on the following: 
+ Calls that start with a positive sentiment score but end negative in the last quarter\.

  If you want to focus on a limited set of contacts to sample for quality assurance, for example, you can look at calls where you know the customer had a positive sentiment at the start but ended with a negative sentiment\. That shows you they left the conversation unhappy about something\. 
+ Calls that start with a negative sentiment score in the first quarter but end positive\.

  Analyzing these calls will help you identify what experiences you can recreate in your contact center\. You can share successful techniques with other agents\.

An additional way of looking at sentiment progression is to check the sentiment trendline\. You can see the variation in the customer's sentiment as the call progresses\. For example, the following images show a conversation with a very low sentiment score in the first quarter of the conversation, and a very positive one at the end\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-sentiment-trend.png)

## How sentiment scores are determined<a name="how-sentiment-scores-are-determined"></a>

To determine the sentiment score, Contact Lens for Amazon Connect analyzes the sentiment for every speaker turn during the conversation\. It uses the frequency and proximity of the resulting sentiment for each speaker turn to assign a score that ranges from \-5 to \+5 for each portion of the call\.

The final sentiment score for the entire conversation is an average of the scores assigned during the call\.