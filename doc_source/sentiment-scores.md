# Investigate sentiment scores during contacts<a name="sentiment-scores"></a>

## What are sentiment scores?<a name="what-are-sentiment-scores"></a>

A sentiment score is an analysis of text, and a rating of whether it includes mostly positive, negative, or neutral language\. Supervisors can use sentiment scores to search conversations and identify contacts that are associated with varying degrees of customer experiences, positive or negative\. It helps them identify which of their contacts to investigate\. 

You can view a sentiment score for the entire conversation, as well as sentiment trend across whole contact\.

## How to investigate sentiment scores<a name="how-to-use-sentiment-scores"></a>

When working to improve your contact center, you may want to focus on the following: 
+ Contacts that start with a positive sentiment score but end with a negative score\.

  If you want to focus on a limited set of contacts to sample for quality assurance, for example, you can look at contacts where you know the customer had a positive sentiment at the start but ended with a negative sentiment\. That shows you they left the conversation unhappy about something\. 
+ Contacts that start with a negative sentiment score but end positive\.

  Analyzing these contacts will help you identify what experiences you can recreate in your contact center\. You can share successful techniques with other agents\.

An additional way of looking at sentiment progression is to check the sentiment trendline\. You can see the variation in the customer's sentiment as the contact progresses\. For example, the following images show a conversation with a very low sentiment score in the beginning of the conversation, and very positive one at the end\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-sentiment-trend.png)

For more information, see [Search for sentiment score or evaluate sentiment shift](search-conversations.md#sentiment-search)\.

## How sentiment scores are determined<a name="how-sentiment-scores-are-determined"></a>

To determine the sentiment score, Contact Lens for Amazon Connect analyzes the sentiment for every part of the conversation of each of the participants\. It uses the frequency and proximity of the resulting sentiment for each participant turn to assign a score that ranges from \-5 to \+5 for each portion of the contact\.

The final sentiment score for the entire conversation is an average of the scores assigned during the contact\.