# About sentiment scores and non\-talk time in Contact Lens<a name="sentiment-scores"></a>

## Sentiment scores<a name="sentiment-scores"></a>

A sentiment score is an analysis of text, and a rating of whether it includes mostly positive, negative, or neutral language\. Supervisors can use sentiment scores to search conversations and identify calls that are associated with varying degrees customer experiences, positive or negative\. It helps them identify which of their calls to investigate\. 

To determine the sentiment score, Contact Lens for Amazon Connect analyzes the sentiment for every speaker turn during the conversation\. It uses the frequency and proximity of the resulting sentiment for each speaker turn to assign a score that ranges from \-5 to \+5 for each portion of the call\.

The final sentiment score for the entire conversation is an average of the scores assigned during the call\.

## Non\-talk time<a name="non-talk-time"></a>

Contact Lens for Amazon Connect also identifies the amount of *non\-talk time******* in a call\. Non\-talk time equals hold time, plus any silence where both participants aren't talking for more than 3 seconds\. This duration can't be customized\.

Non\-talk time can be an indicator of calls that go poorly\. For example, it may indicate that the customer was asking a question that's new for your contact center\. Or it may indicate the agent didn't have a ready answer and needs more training\. 