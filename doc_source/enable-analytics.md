# Enable Contact Lens for Amazon Connect<a name="enable-analytics"></a>

When you enable Contact Lens, it produces a transcript of a call recording\. It analyzes the transcript and gives you sentiment scores\. You can search the transcript for those sentiment scores and keywords to identify calls that you want to investigate\. 

## How to turn on Contact Lens in a contact flow<a name="enable-analytics-contact-flow"></a>

To enable Contact Lens in a contact flow, add a [Set recording and analytics behavior ](set-recording-behavior.md) block to the flow, and configure it for Contact Lens\.

**Tip**  
If you want to continue using Contact Lens to collect data after transferring a contact to another agent or queue, you need to add another [Set recording and analytics behavior ](set-recording-behavior.md) block with **Enable analytics** enabled to the flow\. This is because a transfer generates a second contact ID and CTR\. Contact Lens needs to run on that CTR as well\.

**To enable Contact Lens in a contact flow**

1. Add the [Set recording and analytics behavior ](set-recording-behavior.md) block to a contact flow\.

1. In the contact block, under **Call recording**, choose **On**, **Agent and Customer**\.

   You need both agent and customer call recordings to use Content Lens\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

1. Select **Enable Contact Lens for speech analytics**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior2.png)

1. Choose the language\.

1. Choose **Save**\.

1. If the contact is going to be transferred to another agent or queue, repeat these steps to add another [Set recording and analytics behavior ](set-recording-behavior.md) block with **Enable Contact Lens for speech analytics** 

enabled\.

## How to enable redaction of sensitive data<a name="enable-redaction"></a>

To enable redaction of sensitive data in a contact flow, choose **Redact sensitive data**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-enable-redaction.png)

For examples of an original analyzed file and a redacted file, see [Example Contact Lens output files](contact-lens-example-output-files.md)\.

## Dynamically enable Contact Lens using contact attributes<a name="dynamically-enable-analytics-contact-flow"></a>

You can dynamically enable Contact Lens and the redaction of the output files based on the language of the customer\. For example, for customers using en\-US, you may want only a redacted file whereas for those using en\-GB, you may want both the original and redacted output files\.
+ Redaction: choose one of the following \(case sensitive\)
  + None
  + RedactedOnly
  + RedactedandOriginal
+ Language: choose one of the following \(case sensitive\)
  + en\-US
  + en\-GB
  + en\-IN
  + en\-AU
  + es\-US: Redaction is not supported for this language

You can set these attributes in the following ways:
+ User defined: use a **Set contact attributes** block\. For general instructions about using this block, see [Using a Set contact attributes block](use-attributes-cust-exp.md#use-set-contact-attrib-block)\. Define the **Destination key** and **Value** for redaction and language as needed\. 

  The following image shows how to use contact attributes for redaction:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-contact-attributes-enable-redaction1.png)

  The following image show how to use contact attributes for language:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-contact-attributes-enable-redaction2.png)
+ [Use a Lambda function](use-attributes-cust-exp.md#attribs-with-lambda)\. This is similar to how you set up user\-defined contact attributes\. A Lambda function can return the result as a key\-value pair, depending on the language in which the Lambda function is written\. The following example shows a Lambda function written in JSON: 

  ```
  {
     'redaction_option': 'RedactedOnly',
     'language': 'en-US'
  }
  ```
+ Lex slots contact attributes
+ Lex attributes