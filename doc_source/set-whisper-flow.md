# Contact Block: Set Whisper Flow<a name="set-whisper-flow"></a>

## Contact flow types<a name="set-voice-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="set-voice-description"></a>
+ Overrides the default whisper by linking to a whisper flow you create\.
+ Specifies the whisper to be played to customer on an outbound call, or to the customer or agent when the call is joined\.
+ If this block is triggered during a chat conversation, it has no effect\. There is no whisper\.

## Properties<a name="set-voice-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-whisper-flow-properties2.png)

If you choose to **Select a flow**, you can only select from flows that are type **Agent Whisper** or **Customer Whisper**\.

For information about using attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\.

## Configured block<a name="set-voice-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-whisper-flow-configured.png)