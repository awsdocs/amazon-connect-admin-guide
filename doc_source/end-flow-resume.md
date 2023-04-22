# Flow block: End flow / Resume<a name="end-flow-resume"></a>

## Description<a name="end-flow-resume-description"></a>
+ Ends the current flow without disconnecting the contact\.
+ This block is often used for the **Success** branch of the **Transfer to queue** block\. The flow doesn't end until the call is picked up by an agent\.
+ You also might use this block when a **Loop prompts** block is interrupted\. You can return the customer to the **Loop prompts** block\.

## Supported channels<a name="end-flow-resume-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="end-flow-resume-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Customer queue flow
+ Customer whisper flow
+ Outbound Whisper flow
+ Agent whisper flow

## Properties<a name="end-flow-resume-properties"></a>

The following image shows the **Properties** page of the **End flow / Resume** block\.

![\[The properties page of the End flow Resume block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/end-flow-properties.png)

## Configured block<a name="end-flow-resume-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It does not have any The End flow / Resume termination event branches\.

![\[The properties page of the End flow Resume block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/end-flow-configured.png)