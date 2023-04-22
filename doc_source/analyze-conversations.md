# Analyze conversations using Contact Lens for Amazon Connect<a name="analyze-conversations"></a>

With Contact Lens for Amazon Connect, you can analyze conversations between customers and agents by using speech and chat transcriptions, natural language processing, and intelligent search capabilities\. Contact Lens for Amazon Connect performs sentiment analysis, detects issues, and enables you to automatically categorize contacts\. 

**Speech analytics support**
+ **Real\-time call analytics**: Use to detect and resolve customer issues more proactively while the call is progress\. For example, it can analyze and alert you when a customer is getting frustrated because the agent is unable to resolve a complicated problem\. This allows you to provide more immediate assistance\. 
+ **Post\-call analytics**: Use to understand trends of customer conversations and agent compliance\. This helps you identify opportunities to coach an agent after the call\.

**Chat analytics support**
+ **Post\-chat analytics**: Use to understand trends of customer conversations with both bots and agents\. It provides information specific to a chat interaction, such as the agent greeting time, and agent and customer response times\. The response times and sentiments help you investigate the customer's experience with the bot versus the agent, and identify areas for improvement\. 

You can protect your customer's privacy by redacting sensitive data, such as name, address, and credit card information from transcripts and audio recordings\. 

## Sample Contact details page for a call<a name="sample-contactdetails-call"></a>

The following image shows the summary and conversational analytics for a voice call\. Notice that it includes **Talk time** metrics\.

![\[A sample contact details page with talk time metrics.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contactlens-contactdetails-call1b.png)

The following image shows the next section on the **Contact details** page for a voice call: the audio analysis and transcript\. Notice that personally identifiable information \(PII\) has been [ redacted from the transcript](sensitive-data-redaction.md)\. 

![\[The audio analysis and transcript for the contact.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contactlens-contactdetails-call2b.png)

## Sample Contact details page for a chat<a name="sample-contactdetails-chat"></a>

The following image shows the summary and conversational analytics for a chat\. Notice that it includes chat response metrics, such as **Agent greeting time** \(the time from the agent joining the chat to when they send the first response\), **Customer response time**, and **Agent response time**\.

![\[A contact details page with summary and conversational analytics for a chat.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contactlens-contactdetails-chat1b.png)

The following image shows the next section on the **Contact details** page for a chat: the interaction analysis and transcript\. Notice that you can investigate the customer's interaction with a bot versus the agent\.

![\[The contact details page, the interaction analysis and transcript for a chat.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contactlens-contactdetails-chat2b.png)