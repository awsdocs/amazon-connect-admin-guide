# Update instance settings<a name="update-instance-settings"></a>

To update the instance settings, open the Amazon Connect console, choose the name of the instance from **Instance Alias**, and complete the following procedures\.

Amazon Connect enables agents to hear early media, that is, pre\-connection audio such as busy signals, failure to connect errors, or other informational messages, when making outbound calls\.

**Tip**  
Early media is enabled by default for new instances of Amazon Connect\. If you have an existing instance and want to enable this feature, please open a support ticket\. For instructions, see [Get administrative support for Amazon Connect](get-admin-support.md)\.

**To update the telephony options**

1. In the navigation pane, choose **Telephony**\.

1. \(Optional\) To enable customers to call into your contact center, choose **I want to handle incoming calls with Amazon Connect**\.

1. \(Optional\) To enable outbound calling from your contact center, choose **I want to make outbound calls with Amazon Connect**\.

1. Choose **Save**\.

**To update the data storage settings**

1. In the navigation pane, choose **Data storage**\.

1. \(Optional\) To specify the bucket and KMS key for recordings of voice conversations, choose **Call recordings**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\. 

   When this bucket is created, call recording is enabled at the instance level\. The next step for setting up this functionality is to [set up recording behavior in a contact flow](set-up-recordings.md)\.

1. \(Optional\) To specify the bucket and KMS key for recordings \(transcripts\) of chat conversations, choose **Chat transcripts**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\. 

   When this bucket is created, chat transcripts are enabled at the instance level\. Now all chat transcripts will be stored here\.

1. \(Optional\) To enable live media streaming, choose **Live media streaming**, **Edit**\. For more information, see [Capture customer audio: live media streaming](customer-voice-streams.md)\.

1. \(Optional\) To specify the bucket and KMS key for exported reports, choose **Exported reports**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

**To enable data streaming**

1. In the navigation pane, choose **Data streaming**\.

1. Choose **Enable data streaming**\. For more information, see [Enable data streaming](data-streaming.md)\.

1. For **Contact Trace Records**, do one of the following:
   + Choose **Kinesis Firehose** and select an existing delivery stream, or choose **Create a new Kinesis firehose** to open the Kinesis Firehose console and create the delivery stream\.
   + Choose **Kinesis Stream** and select an existing stream, or choose **Create a new Kinesis firehose** to open the Kinesis console and create the stream\.

1. For **Agent Events**, select an existing Kinesis stream or choose **Create a new Kinesis stream** to open the Kinesis console and create the stream\.

1. Choose **Save**\.

**To update the contact flow settings**

1. In the navigation pane, choose **Contact flows**\.

1. \(Optional\) To add a signing key for use in contact flows, choose **Add key**\. For more information, see [Encrypt customer input](encrypt-data.md)\.

1. \(Optional\) To integrate with Amazon Lex, select a Lex bot\. For more information, see [Add an Amazon Lex bot](amazon-lex.md)\.

1. \(Optional\) To integrate with AWS Lambda, select a Lambda function\. For more information, see [Invoke AWS Lambda functions](connect-lambda-functions.md)\.

1. \(Optional\) To enable contact flow logs, choose **Enable contact flow logs**\. For more information, see [Track events as customers interact with contact flows](about-contact-flow-logs.md)\.