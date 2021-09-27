# Contact block: Check call progress<a name="check-call-progress"></a>

## Description<a name="check-call-progress-description"></a>
+ Engages with the output provided by an answering machine, and provides branches to route the contact accordingly\.
+ It supports the following branches:
  + **Call answered**: The call has been answered by a person\. 
  + **Voicemail \(beep\)**: Amazon Connect identifies that the call ended in a voicemail and it detects a beep\.
  + **Voicemail \(no beep\)**:
    + Amazon Connect identifies that the call ended in a voicemail but it doesn't detect a beep\.
    + Amazon Connect identifies that the call ended in a voicemail, but the beep is unknown\.
  + **Not detected**: Could not detect whether there is voicemail\. This happens when Amazon Connect is unable to make a positive determination of whether a call was answered by a live voice or an answering machine\. Typical situations that land in this state include long silences or excessive background noise\.
  + **Error**: If any errors are encountered due to Amazon Connect not running correctly after media has been established on the call, this is the path that will be taken by the contact flow\. Media is established when the call is either answered by a live voice or by an answering machine\. If the call is rejected by the network or encounters a system error while placing the outbound call, the contact flow will not be run\.

## Supported channels<a name="check-call-progress-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Contact flow types<a name="check-call-progress-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All contact flow types

## Properties<a name="check-call-progress-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-call-progress-properties.png)

## Configured block<a name="check-call-progress-configured-block"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-call-progress-configured.png)