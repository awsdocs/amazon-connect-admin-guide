# Flow block: Set customer queue flow<a name="set-customer-queue-flow"></a>

## Description<a name="set-contact-attributes-description"></a>
+ Specifies the flow to invoke when a customer is transferred to a queue\.

## Supported channels<a name="set-customer-queue-flow-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="set-contact-attributes-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-contact-attributes-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-customer-queue-properties.png)

For information about using attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\.

## Configured block<a name="set-contact-attributes-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-customer-queue-configured.png)

## Sample flows<a name="set-contact-attributes-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample queued callback](sample-queued-callback.md)