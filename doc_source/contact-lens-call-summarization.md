# View call summary<a name="contact-lens-call-summarization"></a>

It can be time\-consuming to review contact transcripts that are hundreds of lines long\. To make this process faster and more efficient, Contact Lens provides the option for you to view a transcript summary\. The summary shows only those lines where Contact Lens has identified an issue, outcome, or action item in the transcript\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-call-summarization.png)

1. Toggle **Show transcript summary** on and off as needed\.

1. **Issue** represents the call driver\. For example, "I'm thinking of upgrading to your online subscription plan\." 

1. **Outcome** represents the likely conclusion or outcome of the contact\. For example, "Based on your current plan I would recommend the online essentials plans that we have\."

1. **Action item** represents the action item the agent takes\. For example, "Please keep an eye out for an email with a price quote\. I will send it to you shortly\."

Each contact has no more than one issue, one outcome, and one action item\. Not all contacts will have all three\. 

**Note**  
If Contact Lens displays the message **There is no summary information for this transcript**, it means no issue, outcome, or action item was identified\.

You don't need to configure call summarization\. It works out\-of\-the\-box without any training of the machine learning model\. 