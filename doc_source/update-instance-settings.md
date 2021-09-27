# Update instance settings<a name="update-instance-settings"></a>

To update the instance settings: 

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. Complete the following procedures\.

## Update telephony options<a name="update-telephony-options"></a>

1. In the navigation pane, choose **Telephony**\.

1. To enable customers to call into your contact center, choose **Receive inbound calls with Amazon Connect**\.

1. To enable outbound calling from your contact center, choose **Make outbound calls with Amazon Connect**\.

1. By enabling early media audio, your agents can hear pre\-connection audio such as busy signals, failure\-to\-connect errors, or other informational messages from telephony providers, when making outbound calls\. Choose **Enable early media**\.

1. Choose **Save**\.

## Update data storage<a name="update-data-storage-options"></a>

1. In the navigation pane, choose **Data storage**\.

1. To specify the bucket and KMS key for recordings of voice conversations, choose **Call recordings**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\. 

   When this bucket is created, call recording is enabled at the instance level\. The next step for setting up this functionality is to [set up recording behavior in a contact flow](set-up-recordings.md)\.

1. To specify the bucket and KMS key for recordings \(transcripts\) of chat conversations, choose **Chat transcripts**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\. 

   When this bucket is created, chat transcripts are enabled at the instance level\. Now all chat transcripts will be stored here\.

1. To enable live media streaming, choose **Live media streaming**, **Edit**\. For more information, see [Capture customer audio: live media streaming](customer-voice-streams.md)\.

1. To specify the bucket and KMS key for exported reports, choose **Exported reports**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. To enable file sharing for both agents and customers, next to **Attachments** choose **Edit**, then **Enable Attachments sharing**\. For more information about this option and additional steps, see [Enable attachments to share files using chat](enable-attachments.md)\.

## Update data streaming options<a name="update-data-streaming-options"></a>

1. In the navigation pane, choose **Data streaming**\.

1. Choose **Enable data streaming**\. For more information, see [Enable data streaming for your instance](data-streaming.md)\.

1. For **Contact Trace Records**, do one of the following:
   + Choose **Kinesis Firehose** and select an existing delivery stream, or choose **Create a new Kinesis Firehose** to open the Kinesis Firehose console and create the delivery stream\.
   + Choose **Kinesis Stream** and select an existing stream, or choose **Create a new Kinesis Firehose** to open the Kinesis console and create the stream\.

1. For **Agent Events**, select an existing Kinesis stream or choose **Create a new Kinesis Stream** to open the Kinesis console and create the stream\.

1. Choose **Save**\.

## Update analytics tools options<a name="update-analytics-tools"></a>

1. In the navigation pane, choose **Analytics tools**\.

1. Choose **Enable Contact Lens**\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\.

1. Choose **Save**\.

## Update contact flow settings<a name="update-contact-flow-settings"></a>

1. In the navigation pane, choose **Contact flows**\.

1. \(Optional\) To add a signing key for use in contact flows, choose **Add key**\. For more information, see [Encrypt customer input](encrypt-data.md)\.

1. \(Optional\) To integrate with Amazon Lex, select a Lex bot\. For more information, see [Add an Amazon Lex bot](amazon-lex.md)\.

1. \(Optional\) To integrate with AWS Lambda, select a Lambda function\. For more information, see [Invoke AWS Lambda functions](connect-lambda-functions.md)\.

1. \(Optional\) To enable contact flow logs, choose **Enable Contact flow logs**\. For more information, see [Track events as customers interact with contact flows](about-contact-flow-logs.md)\.

1. \(Optional\) To use the best available voice from Amazon Polly, choose **Use the best available voice**\. For more information, see [Amazon Polly best sounding voice](text-to-speech.md#amazon-polly-best-sounding-voice)\.

1. \(Optional\) Use the voices available in Amazon Polly\.