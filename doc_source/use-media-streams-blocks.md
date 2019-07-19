# Example Contact Flow for Testing Live Media Streaming<a name="use-media-streams-blocks"></a>

In a contact flow, add a **Start media streaming** block in the flow at the point where you want to enable customer audio streaming\. Connect the **Success** branch to the rest of your flow\. When you want to stop customer media streaming, add a **Stop media streaming** block to the flow\. Customer audio is captured until a **Stop media streaming** block is invoked, even if the contact is passed to another contact flow\.

Use the contact attributes for media streaming in your contact flow so that the CTR includes the attributes\. You can then view the CTR to determine the media streaming data associated with a specific contact\. You can also pass the attributes to an AWS Lambda function\.

The following example contact flow demonstrates using media streaming with attributes for testing purposes\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/media-streaming-flow.png)

After the audio is successfully streamed to Kinesis Video Streams, the contact attributes are populated from the **Invoke AWS Lambda function** block\. You can use the attributes to identify the location in the stream where the customer audio starts\. For instructions, see [Live Media Streaming Contact Attributes](media-streaming-attributes.md)\.