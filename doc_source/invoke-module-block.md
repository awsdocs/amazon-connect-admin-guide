# Flow block: Invoke module<a name="invoke-module-block"></a>

## Description<a name="invoke-module-block-description"></a>

Calls a published module, which enables you create reusable sections of a contact flow\.

For more information, see [Flow modules for reusable functions](contact-flow-modules.md)\.

## Supported channels<a name="invoke-lambda-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="invoke-module-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow

## Properties<a name="invoke-module-block-properties"></a>

The following image shows the **Properties** page of the **Invoke module** block\.

![\[The properties page of the Invoke module block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/invoke-module-properties.png)

## Configured block<a name="invoke-module-block-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has two branches: **Success** and **Error**\.

![\[A configured Invoke module block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/invoke-module-configured.png)