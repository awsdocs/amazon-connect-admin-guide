# Contact block: Set callback number<a name="set-callback-number"></a>

## Description<a name="set-callback-number-description"></a>
+ Specify the attribute to set the callback number\.

## Contact flow types<a name="set-callback-number-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-callback-number-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callback-number.png)

## Configuration tips<a name="set-callback-number-tips"></a>
+ The [Store customer input](store-customer-input.md) block often comes before this block\. It stores the customer's callback number\.

## Configured block<a name="set-callback-number-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callback-number-configured.png)

1. The customer entered phone number that is not valid\.

1. Amazon Connect is unable to dial that number\. For example, if your instance is not allowed to make calls to \+447 prefix phone numbers, and the customer requested callback to a \+447 prefix number\. Even though number is valid, Amazon Connect cannot call it\. 

## Sample flows<a name="set-callback-number-samples"></a>

 See these sample flows for scenarios that use this block:
+ [Sample queue configurations](sample-queue-configurations.md)
+ [Sample queued callback](sample-queued-callback.md): this sample only applies to previous instances of Amazon Connect\.

## Scenarios<a name="set-callback-number-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up queued callback](setup-queued-callback.md)
+ [About queued callbacks in metrics](about-queued-callbacks.md)