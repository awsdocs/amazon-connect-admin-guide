# Example Contact Flow for Testing Live Media Streaming<a name="use-media-streams-blocks"></a>

Here's how you can set up a contact flow to test live media streaming: 

1. Add a **Start media streaming** block at the point where you want to enable customer audio streaming\.

1. Connect the **Success** branch to the rest of your flow\.

1. Add a **Stop media streaming** block to where you want to stop streaming\. 

1. Configure both blocks to specify what you want to stream: **From the customer** and/or **To the customer**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/start-media-streaming.png)

Customer audio is captured until a **Stop media streaming** block is invoked, even if the contact is passed to another contact flow\.

Use the contact attributes for media streaming in your contact flow so that the CTR includes the attributes\. You can then view the CTR to determine the media streaming data associated with a specific contact\. You can also pass the attributes to an AWS Lambda function\.

The following example contact flow shows how you might use media streaming with attributes for testing purposes\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/media-streaming-flow.png)

After the audio is successfully streamed to Kinesis Video Streams, the contact attributes are populated from the **Invoke AWS Lambda function** block\. You can use the attributes to identify the location in the stream where the customer audio starts\. For instructions, see [Contact Attributes for Live Media Streaming](media-streaming-attributes.md)\.