# Update Instance Settings<a name="update-instance-settings"></a>

To update the instance settings, open the Amazon Connect console, choose the name of the instance from **Instance Alias**, and complete the following procedures\.

**To update the telephony options**

1. In the navigation pane, choose **Telephony**\.

1. \(Optional\) To enable customers to call into your contact center, choose **I want to handle incoming calls with Amazon Connect**\.

1. \(Optional\) To enable outbound calling from your contact center, choose **I want to make outbound calls with Amazon Connect**\.

1. Choose **Save**\.

**To update the data storage settings**

1. In the navigation pane, choose **Data storage**\.

1. \(Optional\) To specify the bucket and KMS key for recordings of voice conversations, choose **Call recordings**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. \(Optional\) To specify the bucket and KMS key for recordings \(transcripts\) of chat conversations, choose **Chat transcripts**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. \(Optional\) To enable live media streaming, choose **Live media streaming**, **Edit**\. For more information, see [Capture Customer Audio: Live Media Streaming](customer-voice-streams.md)\.

1. \(Optional\) To specify the bucket and KMS key for exported reports, choose **Exported reports**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

**To enable data streaming**

1. In the navigation pane, choose **Data streaming**\.

1. Choose **Enable data streaming**\. For more information, see [Enable Data Streaming](data-streaming.md)\.

1. For **Contact Trace Records**, do one of the following:
   + Choose **Kinesis Firehose** and select an existing delivery stream, or choose **Create a new Kinesis firehose** to open the Kinesis Firehose console and create the delivery stream\.
   + Choose **Kinesis Stream** and select an existing stream, or choose **Create a new Kinesis firehose** to open the Kinesis console and create the stream\.

1. For **Agent Events**, select an existing Kinesis stream or choose **Create a new Kinesis stream** to open the Kinesis console and create the stream\.

1. Choose **Save**\.

**To update the contact flow settings**

1. In the navigation pane, choose **Contact flows**\.

1. \(Optional\) To add a signing key for use in contact flows, choose **Add key**\. For more information, see [Encrypt Customer Input](contact-flow-keys.md)\.

1. \(Optional\) To integrate with Amazon Lex, select a Lex bot\. For more information, see [Add an Amazon Lex Bot](amazon-lex.md)\.

1. \(Optional\) To integrate with AWS Lambda, select a Lambda function\. For more information, see [Invoke AWS Lambda Functions](connect-lambda-functions.md)\.

1. \(Optional\) To enable contact flow logs, choose **Enable contact flow logs**\. For more information, see [Contact Flow Logs](contact-flow-logs.md)\.