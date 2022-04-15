# Enable data streaming for your instance<a name="data-streaming"></a>

You can export contact records and agent events from Amazon Connect and perform real\-time analysis on contacts\. Data streaming sends data to Amazon Kinesis\.

**To enable data streaming for your instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the **Instances** page, choose the instance alias\. The instance alias is also your instance name, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Data streaming**\.

1. Choose **Enable data streaming**\.

1. For **Contact records**, do one of the following:
   + Choose **Kinesis Firehose** and select an existing delivery stream, or choose **Create a new Kinesis firehose** to open the Kinesis Firehose console and create the delivery stream\.
   + Choose **Kinesis Stream** and select an existing stream, or choose **Create a Kinesis stream** to open the Kinesis console and create the stream\.

1. For **Agent Events**, select an existing Kinesis stream or choose **Create a new Kinesis stream** to open the Kinesis console and create the stream\.

1. Choose **Save**\.

## Using server\-side encryption for the Kinesis stream<a name="server-side-encryption-data-stream"></a>

If you enable server\-side encryption for the Kinesis stream you select, Amazon Connect cannot publish to the stream because it does not have permission to call `kms:GenerateDataKey` so that it can encrypt data sent to Kinesis\. To work\-around this, do the following steps: 

1. Enable encryption for recordings of conversations or scheduled reports\.

1. Create a customer managed key to use for encryption\.

1. Choose the same customer managed key for the Kinesis data stream that you use for scheduled reports or recordings of conversations\.

   For more information, see [Creating Keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) in the *AWS Key Management Service Developer Guide*\.