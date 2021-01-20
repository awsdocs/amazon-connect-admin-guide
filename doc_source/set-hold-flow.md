# Contact block: Set hold flow<a name="set-hold-flow"></a>

## Description<a name="set-hold-flow-description"></a>
+ Links from one contact flow type to another\.
+ Specifies the flow to invoke when a customer or agent is put on hold\.

  If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\.

## Contact flow types<a name="set-hold-flow-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Outbound whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-hold-flow-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-hold-flow-properties.png)

For information about using attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\.

## Configured block<a name="set-hold-flow-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-hold-flow-configured.png)