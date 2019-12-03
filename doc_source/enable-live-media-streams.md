# Enable Live Media Streaming in Your Instance<a name="enable-live-media-streams"></a>

Live media streaming \(customer audio streams\) is not enabled by default\. You can enable customer audio streams from the settings page for your instance\.

**To enable live media streaming**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the instance alias for the instance from the **Instance Alias** column\.

1. In the navigation pane, choose **Data storage**\.

1. Under **Live media streaming**, choose **Edit**\. Choose **Enable live media streaming**\.

1. Enter a prefix for the Kinesis Video Streams created for your customer audio\. This prefix makes it easier for you to identify the stream with the data\.

1. Choose the KMS master key to use to encrypt the data sent to Kinesis\.

1. Specify a number and unit for the **Data retention period**\. If you select **No data retention**, data is not retained and can be used only for immediate consumption\.

1. Choose **Save** under **Live media streaming**, and then choose **Save** at the bottom of the page\.

After you enable live media streaming, add **Start media streaming** and **Stop media streaming** blocks to your contact flow\. Configure those blocks to specify what audio you want to capture\. For instructions and an example, see [Example Contact Flow for Testing Live Media Streaming](use-media-streams-blocks.md)\.