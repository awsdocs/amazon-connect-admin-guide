# Flow block: Set callback number<a name="set-callback-number"></a>

## Description<a name="set-callback-number-description"></a>
+ Specify the attribute to set the callback number\.

## Supported channels<a name="set-callback-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Flow types<a name="set-callback-number-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-callback-number-properties"></a>

The following image shows the **Properties** page of the **Set callback number** block\.

![\[The properties page of the Set callback number block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callback-number.png)

## Configuration tips<a name="set-callback-number-tips"></a>
+ The [Store customer input](store-customer-input.md) block often comes before this block\. It stores the customer's callback number\.

## Configured block<a name="set-callback-number-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has the following branches: **Success**, **Invalid number**, and **Not dialable**\.

![\[A configured Set callback number block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callback-number-configured.png)

1. **Invalid number**: The customer entered phone number that is not valid\.

1. **Not dialable**: Amazon Connect is unable to dial that number\. For example, if your instance is not allowed to make calls to \+447 prefix phone numbers, and the customer requested callback to a \+447 prefix number\. Even though number is valid, Amazon Connect cannot call it\. 

## Sample flows<a name="set-callback-number-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample queue configurations](sample-queue-configurations.md)
+ [Sample queued callback](sample-queued-callback.md): this sample only applies to previous instances of Amazon Connect\.

## Scenarios<a name="set-callback-number-scenarios"></a>

See these topics for scenarios that use this block:
+ [](setup-queued-cb.md)
+ [About queued callbacks in metrics](about-queued-callbacks.md)