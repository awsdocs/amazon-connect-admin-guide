# Contact Block: Start Media Streaming<a name="start-media-streaming"></a>

## Contact flow types<a name="start-media-streaming-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Customer Whisper flow
+ Outbound Whisper flow
+ Agent Whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="start-media-streaming-description"></a>

Captures what the customer hears and says during a contact\. You can then perform analysis on the audio streams to:
+ Determine customer sentiment\.
+ Use the audio for training purposes\.
+ Identify and flag abusive callers\.

## Properties<a name="start-media-streaming-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/start-media-streaming.png)

## Configuration tips<a name="start-media-streaming-tips"></a>
+ You must enable live media streaming in your instance to successfully capture customer audio\. For instructions, see [Capture customer audio: live media streaming](customer-voice-streams.md)\.
+ Customer audio is captured until a **Stop media streaming** block is invoked, even if the contact is passed to another contact flow\.
+ You must use a **Stop media streaming** block to stop media streaming\.
+ If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\.

## Configured block<a name="start-media-streaming-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/start-media-streaming-configured.png)

## Sample flows<a name="start-media-streaming-samples"></a>

[Example contact flow for testing live media streaming](use-media-streams-blocks.md) 