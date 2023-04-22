# Update instance settings<a name="update-instance-settings"></a>

To update the instance settings: 

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\. The following image shows the **Amazon Connect virtual contact center instances** page, with a box a box around the instance alias\.  
![\[The Amazon Connect virtual contact center instances page, the instance alias.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. Complete the following procedures\.

## Update telephony options<a name="update-telephony-options"></a>

1. In the navigation pane, choose **Telephony**\.

1. To enable customers to call into your contact center, choose **Receive inbound calls with Amazon Connect**\.

1. To enable outbound calling from your contact center, choose **Make outbound calls with Amazon Connect**\.

1. To enable outbound campaigns, choose **Enable outbound campaigns**\.

1. By enabling early media audio, your agents can hear pre\-connection audio such as busy signals, failure\-to\-connect errors, or other informational messages from telephony providers, when making outbound calls\. Choose **Enable early media**\.

1. By default, you can have three participants on a call \(for example, two agents and a customer, or an agent, a customer, and an external party\)\. To enable multi\-party calls with more participants, choose **Enable up to six parties on a call**\. This feature is only available in CCPv2\.

1. Choose **Save**\.

## Update data storage<a name="update-data-storage-options"></a>
+ In the navigation pane, choose **Data storage**\. Choose the following:
  + **Call recordings**: Choose **Edit**, specify the bucket and KMS key for recordings of voice conversations, and then choose **Save**\. 

    When this bucket is created, call recording is enabled at the instance level\. The next step for setting up this functionality is to [set up recording behavior in a contact flow](set-up-recordings.md)\.
  + **Chat transcripts**: Choose **Edit**, specify the bucket and KMS key for recordings \(transcripts\) of chat conversations, and then choose **Save**\. 

    When this bucket is created, chat transcripts are enabled at the instance level\. Now all chat transcripts will be stored here\.
  + **Live media streaming**: Choose **Edit** to enable live media streaming, choose **Edit**\. For more information, see [Capture customer audio: live media streaming](customer-voice-streams.md)\.
  + **Exported reports**: Choose **Edit**, specify the bucket and KMS key for exported reports, and then choose **Save**\. 
  + **Attachments**: Choose **Edit**, then **Enable Attachments sharing** to enable file sharing for both agents and customers\. For more information about this option and additional steps, see [Enable attachments to share files using chat](enable-attachments.md)\. 
  + **Contact evaluations**: Choose **Edit**, specify the bucket and KMS key for performance evaluations, and then choose **Save**\. 

    When this bucket is created, evaluations are enabled at the instance level\. The next step for setting up this feature is to [create an evaluation form](create-evaluation-forms.md)\.

## Update data streaming options<a name="update-data-streaming-options"></a>

1. In the navigation pane, choose **Data streaming**\.

1. Choose **Enable data streaming**\. For more information, see [Enable data streaming for your instance](data-streaming.md)\.

1. For **Contact records**, do one of the following:
   + Choose **Kinesis Firehose** and select an existing delivery stream, or choose **Create a new Kinesis Firehose** to open the Kinesis Firehose console and create the delivery stream\.
   + Choose **Kinesis Stream** and select an existing stream, or choose **Create a new Kinesis Firehose** to open the Kinesis console and create the stream\.

1. For **Agent Events**, select an existing Kinesis stream or choose **Create a new Kinesis Stream** to open the Kinesis console and create the stream\.

1. Choose **Save**\.

## Update analytics tools options<a name="update-analytics-tools"></a>

1. In the navigation pane, choose **Analytics tools**\.

1. Choose **Enable Contact Lens**\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\.

1. Choose **Save**\.

## Update flow settings<a name="update-contact-flow-settings"></a>

1. In the navigation pane, choose **Flows**\.

1. \(Optional\) To add a signing key for use in flows, choose **Add key**\. For more information, see [Encrypt customer input](encrypt-data.md)\.

1. \(Optional\) To integrate with Amazon Lex, select a Lex bot\. For more information, see [Add an Amazon Lex bot to Amazon Connect](amazon-lex.md)\.

1. \(Optional\) To integrate with AWS Lambda, select a Lambda function\. For more information, see [Invoke AWS Lambda functions](connect-lambda-functions.md)\.

1. \(Optional\) To enable flow logs, choose **Enable flow logs**\. For more information, see [Track events as customers interact with flows](about-contact-flow-logs.md)\.

1. \(Optional\) To use the best available voice from Amazon Polly, choose **Use the best available voice**\. For more information, see [Amazon Polly best sounding voice](text-to-speech.md#amazon-polly-best-sounding-voice)\.

1. \(Optional\) Use the voices available in Amazon Polly\.