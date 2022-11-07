# Enable live media streaming in your instance<a name="enable-live-media-streams"></a>

Live media streaming \(customer audio streams\) is not enabled by default\. You can enable customer audio streams from the settings page for your instance\.

**To enable live media streaming**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.

1. In the navigation pane, choose **Data storage**\.

1. Under **Live media streaming**, choose **Edit**\. Choose **Enable live media streaming**\.

1. Enter a prefix for the Kinesis Video Streams created for your customer audio\. This prefix makes it easier for you to identify the stream with the data\.

1. Choose the KMS key to use to encrypt the data sent to Kinesis\. The KMS key must be in the same Region as the instance\. 

1. Specify a number and unit for the **Data retention period**\. If you select **No data retention**, data is not retained and can be used only for immediate consumption\.

1. Choose **Save** under **Live media streaming**, and then choose **Save** at the bottom of the page\.

After you enable live media streaming, add **Start media streaming** and **Stop media streaming** blocks to your flow\. Configure those blocks to specify what audio you want to capture\. For instructions and an example, see [Example flow for testing live media streaming](use-media-streams-blocks.md)\.