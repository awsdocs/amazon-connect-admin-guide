# Contact Block: End Flow / Resume<a name="end-flow-resume"></a>

## Contact flow types<a name="end-flow-resume-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Customer queue flow
+ Customer whisper flow
+ Outbound Whisper flow
+ Agent whisper flow

## Description<a name="end-flow-resume-description"></a>
+ Ends the current flow without disconnecting the contact\.
+ This block is often used for the **Success** branch of the **Transfer to queue** block\. The flow doesn't end until the call is picked up by an agent\.
+ You also might use this block when a **Loop prompts** block is interrupted\. You can return the customer to the **Loop prompts** block\.

## Properties<a name="end-flow-resume-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/end-flow-properties.png)

## Configured block<a name="end-flow-resume-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/end-flow-configured.png)