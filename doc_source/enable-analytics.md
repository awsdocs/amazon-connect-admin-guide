# Enable Contact Lens for Amazon Connect<a name="enable-analytics"></a>

You can enable Contact Lens for Amazon Connect in a few steps\. Add a [Set recording and analytics behavior](set-recording-behavior.md) block to a flow, and configure it to enable Contact Lens for voice, chat, or both\.

The following image shows a block that's configured for call recording, and Contact Lens speech analytics and chat analytics\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

The procedures in this topic describe the steps to enable Contact Lens for call or chat analytics\.

## Important things to know<a name="important-set-behaviorblock"></a>
+ **Collect data after transferring a contact**: If you want to continue using Contact Lens to collect data after transferring a contact to another agent or queue, you need to add another [Set recording and analytics behavior](set-recording-behavior.md) block with **Enable analytics** enabled for the flow\. This is because a transfer generates a second contact ID and contact record\. Contact Lens needs to run on that contact record as well\.
+ When you select **Enable Contact Lens conversational analytics**, you must choose to enable speech or chat analytics\. Otherwise, your flow will display an error when you publish it\.
+ Where you place the [Set recording and analytics behavior](set-recording-behavior.md) block in a flow affects the agent's experience with contact summarization\. For more information, see [Design a flow for call summarization](#call-summarization-agent)\.

## Enable call recording and speech analytics<a name="enable-callrecording-speechanalytics"></a>

1. In the [Set recording and analytics behavior](set-recording-behavior.md) block, under **Call recording**, choose **On**, **Agent and Customer**\.

   Both agent and customer call recordings are required to use Contact Lens for voice contacts\.

1. Under **Analytics**, choose **Enable Contact Lens conversational analytics**, **Enable speech analytics**\. 

   If you don't see this option, Contact Lens for Amazon Connect hasn't been enabled for your instance\. To enable it, see [Update instance settings](update-instance-settings.md)\.

1. Choose one of the following:

   1. **Post\-call analytics**: Contact Lens analyzes the call recording after the conversation and After Contact Work \(ACW\) is complete\. This option provides the best transcription accuracy\.

   1. **Real\-time analytics**: Contact Lens provides both real\-time insights during the call, and post\-call analytics after the conversation has ended and After Contact Work \(ACW\) is complete\.

      If you choose this option, we recommend setting up alerts based on keywords and phrases that the customer may utter during the call\. Contact Lens analyzes the conversation real\-time to detect the specified keywords or phrases, and alerts supervisors\. From there, supervisors can listen in on the live call and provide guidance to the agent to help them resolve the issue faster\.

      For information about setting up alerts, see [Alert supervisors in real\-time based on keywords and phrases](add-rules-for-alerts.md)\.

      If your instance was created before October 2018, additional configuration is needed to access real\-time call analytics\. For more information, see [Service\-linked role permissions for Amazon Connect](connect-slr.md#slr-permissions)\.

1. Choose the language\. For a list of available languages for various Contact Lens features, see [Supported languages](supported-languages.md)\.

   For instructions on using an attribute, see [Use contact attributes](#dynamically-enable-analytics-contact-flow)\.

1. Optionally, enable redaction of sensitive data\. For more information, see the next section, [Enable redaction](#enable-redaction)\.

1. Choose **Save**\.

1. If the contact is going to be transferred to another agent or queue, repeat these steps to add another [Set recording and analytics behavior](set-recording-behavior.md) block with **Enable Contact Lens for conversational analytics** enabled\. 

## Enable chat analytics<a name="enable-chatanalytics"></a>

1. In the [Set recording and analytics behavior](set-recording-behavior.md) block, under **Analytics**, choose **Enable Contact Lens conversational analytics**, and **Enable chat analytics**\.

   If you don't see this option, Contact Lens for Amazon Connect hasn't been enabled for your instance\. To enable it, see [Update instance settings](update-instance-settings.md)\.

1. Choose the language\. For a list of available languages for various Contact Lens features, see [Supported languages](supported-languages.md)\.

   For instructions on using an attribute, see [Use contact attributes](#dynamically-enable-analytics-contact-flow)\.

1. Optionally, enable redaction of sensitive data\. For more information, see the next section, [Enable redaction of sensitive data](#enable-redaction)\.

1. Choose **Save**\.

1. If the contact is going to be transferred to another agent or queue, repeat these steps to add another [Set recording and analytics behavior](set-recording-behavior.md) block with **Enable Contact Lens for conversational analytics** enabled\. 

## Enable redaction of sensitive data<a name="enable-redaction"></a>

To enable redaction of sensitive data in a flow, choose **Redact sensitive data**\. When redaction is enabled you can choose from the following options:
+ Redact all personally identifiable information \(PII\) data \(all PII entities supported\)\.
+ Choose which PII entities to redact from the list of supported entities\.

 If you accept the default settings, Contact Lens redacts all personally identifiable information \(PII\) it identifies, and replaces it with **\[PII\]** in the transcript\. This option is shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-enable-redaction-default.png)

### Select PII entities to redact<a name="select-pii-entities-redact"></a>

Under the **Data redaction** section, you can select specific PII entities to redact, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-select-entities-to-redact.png)

### Choose data redaction replacement<a name="mask-pii"></a>

Under the **Data redaction replacement** section, you can choose the mask to be used as data redaction replacement, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-dataredactionreplacement.png)

For more information about using redaction, see [Use sensitive data redaction](sensitive-data-redaction.md)\.

## Review sensitive data redaction for accuracy<a name="review-sensitive-data-redaction"></a>

The redaction feature is designed to identify and remove sensitive data\. However, due to the predictive nature of machine learning, it may not identify and remove all instances of sensitive data in a transcript generated by Contact Lens\. We recommend you review any redacted output to ensure it meets your needs\.

**Important**  
The redaction feature does not meet the requirements for de\-identification under medical privacy laws like the U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\), so we recommend you continue to treat it as protected health information after redaction\.

For the location of redacted files and examples, see [Output file locations](example-contact-lens-output-locations.md)\.

## Dynamically enable Contact Lens using contact attributes<a name="dynamically-enable-analytics-contact-flow"></a>

You can dynamically enable Contact Lens and the redaction of the output files based on the language of the customer\. For example, for customers using en\-US, you may want only a redacted file whereas for those using en\-GB, you may want both the original and redacted output files\.
+ Redaction: choose one of the following \(they are case sensitive\)
  + None
  + RedactedOnly
  + RedactedAndOriginal
+ Language: Choose from the [list of available languages](supported-languages.md#supported-languages-contact-lens)\.

You can set these attributes in the following ways:
+ User defined: use a **Set contact attributes** block\. For general instructions about using this block, see [How to reference contact attributes](how-to-reference-attributes.md)\. Define the **Destination key** and **Value** for redaction and language as needed\. 

  The following image shows how to use contact attributes for redaction\. Note that **Value** is case sensitive\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-contact-attributes-enable-redaction1.png)

  The following image show how to use contact attributes for language:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-contact-attributes-enable-redaction2.png)
+ [Use a Lambda function](attribs-with-lambda.md)\. This is similar to how you set up user\-defined contact attributes\. An AWS Lambda function can return the result as a key\-value pair, depending on the language of the Lambda response\. The following example shows a Lambda response in JSON: 

  ```
  {
     'redaction_option': 'RedactedOnly',
     'language': 'en-US'
  }
  ```

## Design a flow for call summarization<a name="call-summarization-agent"></a>

Transcripts are visible to agents using the Contact Control Panel \(CCP\) depending on whether Contact Lens analytics is enabled in the [Set recording and analytics behavior](set-recording-behavior.md) in the inbound flow, and/or a transfer flow\.

This section provides three use cases for enabling Contact Lens analytics in the [Set recording and analytics behavior](set-recording-behavior.md) block, and describes how they affect the agent's experience with contact summarization\.

### Use case 1: Contact Lens analytics is enabled in an inbound flow only<a name="call-summarization-inbound-notransfer"></a>
+ A contact enters the inbound flow, and there are no call transfers\. Following is the agent experience:

  The agent receives the full transcript during After Contact Work \(ACW\)\. The transcript includes everything said by the agent and the customer, from the moment the agent accepts the initial call, until the call has ended, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use1.png)
+ A contact enters the inbound flow, and there is a call transfer\. Following is the agent experience:
  + Agent 1 receives a call transcript after they leave the conference/warm transfer, during ACW\.

    The transcript includes everything said by agent 1 and the customer, from the moment the agent accepts the initial call, until the agent 1 leaves the conference/warm transfer portion of the call\. The transcript includes the flow \(transfer/queue flow\) prompt messages, as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use2.png)
  + Agent 2 receives a call transcript at the time of accepting the conference/warm transfer call from agent 1\.

    The transcript includes everything said by agent 1 and the customer, from the moment agent 1 accepts the initial call until the agent 1 leaves the conference/warm transfer portion of the call\. The transcript includes the flow \(transfer/queue flow\) prompt messages, and the warm transfer conversation, as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use2b.png)

    Because Contact Lens is not enabled in the transfer flow, agent 2 doesn't see the remainder of the transcript when the call has ended and they enter ACW, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use2c.png)

### Use case 2: Contact Lens analytics is enabled in an inbound flow and a transfer flow \(quick connect\)<a name="call-summarization-inbound-transfer2"></a>
+ A contact enters the inbound flow, and there are no call transfers\. Following is the agent experience:
  + Agent 1 receives a full call transcript \(unredacted\) during ACW\. 

    The transcript includes everything said by agent 1 and the customer from the moment the agent accepts the call, until the call has ended\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use3.png)
+ A contact enters the inbound flow, and there is a call transfer\. Following is the agent experience:
  + Agent 1 receives a call transcript after they leave the conference/warm transfer, during ACW\.

    The transcript includes everything said by agent 1 and the customer from the moment agent 1 accepts the call, until agent 1 leaves the conference/warm transfer portion of the call\. The transcript includes flow \(transfer/queue flow\) prompt messages\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use2b.png)
  + Agent 2 receives a call transcript at the time of accepting the conference/warm transfer call from agent 1\.

    The transcript includes everything said by agent 1 and the customer, from the moment agent 1 accepts the call, until agent 1 leaves the conference/warm transfer portion of the call\. The transcript includes the flow \(transfer/queue flow\) prompt messages\. 
  + Because Contact Lens is enabled in the transfer flow, agent 2 receives a call transcript after the call is completed, during ACW\. 

    The transcript includes only the remaining portion of the call between agent 2 and customer, after agent 1 has left the call\. The transcript includes everything said by agent 2 and the customer, from the moment they are conferenced/warm transferred in, until the call has ended\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-summarization-use3b.png)

## What if the flow block fails to enable Contact Lens?<a name="troubleshoot-contactlens-enablement"></a>

It's possible that the [Set recording and analytics behavior](set-recording-behavior.md) block can fail to enable Contact Lens on a contact\. If Contact Lens isn't enabled for a contact, [check the flow logs](search-contact-flow-logs.md) for the error\.

## Multi\-party calls and Contact Lens<a name="multiparty-calls-contactlens"></a>

We do not support multi\-party calls in Contact Lens\. For example, if there are more than two parties \(agent and customer\) on a call, the quality of the transcription and analytics, such as sentiment and categories, is degraded\.