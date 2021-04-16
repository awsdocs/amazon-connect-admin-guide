# Contact block: Check contact attributes<a name="check-contact-attributes"></a>

## Description<a name="check-contact-attributes-description"></a>
+ Branches based on a comparison to the value of a contact attribute\.
+ Supported comparisons include: **Equals**, **Is Greater Than**, **Is Less Than**, **Starts With**, **Contains**\.

## Contact flow types<a name="check-contact-attributes-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="check-contact-attributes-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-properties.png)

### Conditions to check can be dynamic<a name="check-dynamic-attributes"></a>

You can check conditions like the following:
+ $\.Attributes\.verificationCode

## Configuration tips<a name="check-contact-attributes-tips"></a>

If you have multiple conditions to compare, Amazon Connect checks them in the order they are listed\. 

For example, in the following image Amazon Connect compares the **greater than 60** condition first and compares **greater than 2** last\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-tips-order-conditions-are-checked.png)

## Configured<a name="check-contact-attributes-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-configured.png)

## Sample flows<a name="check-contact-attributes-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)
+  [Sample interruptible queue flow with callback](sample-interruptible-queue.md)

## Scenarios<a name="check-contact-attributes-scenarios"></a>

See these topics for scenarios that use this block:
+ [How to reference contact attributes](how-to-reference-attributes.md)
+ [Route based on contact's channel](use-channel-contact-attribute.md)
+ [How to reference contact attributes](how-to-reference-attributes.md)