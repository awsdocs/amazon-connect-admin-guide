# View contact summarization<a name="contact-lens-call-summarization"></a>

It can be time\-consuming to review contact transcripts that are hundreds of lines long\. To make this process faster and more efficient, Contact Lens provides the option for managers to view a transcript summary on the **Contact details** page, and for agents to view a transcript summary in the Contact Control Panel \(CCP\)\. 

**Tip**  
For a list of supported languages, see the **Contact summarization** column in [Contact Lens for Amazon Connect](supported-languages.md#supported-languages-contact-lens)\.

After you [enable Contact Lens](enable-analytics.md), it identifies key parts of the customer conversation, assigns a label \(for example, issue, outcome, or action item\), and displays a summary that you can expand to view the full transcript of the contact\. The summary shows only those lines where Contact Lens has identified an issue, outcome, or action item in the transcript\. 

Following is an example of contact summarization on the **Contact details** page\. 

![\[The contact detail page, the contact summarization.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-call-summarization.png)

1. Toggle **Show transcript summary** on and off as needed\.

1. **Issue** represents the contact driver\. For example, "I'm thinking of upgrading to your online subscription plan\." 

1. **Outcome** represents the likely conclusion or outcome of the contact\. For example, "Based on your current plan I would recommend the online essentials plans that we have\."

1. **Action item** \(not shown\) represents the action item the agent takes\. For example, "Please keep an eye out for an email with a price quote\. I will send it to you shortly\."

Each contact has no more than one issue, one outcome, and one action item\. Not all contacts will have all three\. 

**Note**  
If Contact Lens displays the message **There is no summary information for this transcript**, it means no issue, outcome, or action item was identified\.

To learn about the agent's experience with contact summarization—what part of the transcript is displayed in the Contact Control Panel, and when—see [Design a flow for call summarization](enable-analytics.md#call-summarization-agent)\.