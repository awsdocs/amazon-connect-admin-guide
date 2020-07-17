# Contact block: Distribute by percentage<a name="distribute-by-percentage"></a>

## Contact flow types<a name="disconnect-hang-up-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Outbound Whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="disconnect-hang-up-description"></a>
+ This block is useful for doing A/B testing\. It routes customers randomly based on a percentage\.
+ Like flipping a coin, contacts are distributed randomly, which doesn’t guarantee exact percentage splits\.

## Properties<a name="disconnect-hang-up-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/distribute-by-percentage-properties.png)

## How it works<a name="disconnect-hang-up-works"></a>

This block creates static allocation rules based on how you configure it\. Internal logic generates a random number between 1\-100\. This number identifies which branch to take\. It doesn't use current or historical volume as part of it's logic\.

For example, say a block is configure like this:
+ 20% = A
+ 40% = B
+ 40% remaining = Default

When contact a is being routed through a flow, Amazon Connect generates the random number\. 
+ If number is between 0\-20, the contact is routed down the A branch\.
+ Between 21\-60 it's routed down the B branch\.
+ Greater than 60 it's routed down the Default branch\.

## Configured block<a name="disconnect-hang-up-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/distribute-by-percentage-configured.png)

## Sample flows<a name="disconnect-hang-up-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample AB test](sample-ab-test.md)