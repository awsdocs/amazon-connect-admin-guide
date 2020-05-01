# Contact Block: Distribute by Percentage<a name="distribute-by-percentage"></a>

## In contact flow types<a name="disconnect-hang-up-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Generic contact flow
+ Customer queue flow
+ Outbound Whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="disconnect-hang-up-description"></a>
+ This block is useful for doing A/B testing\. It routes customers randomly based on a percentage\.
+ Like flipping a coin, contacts are distributed randomly, which doesn’t guarantee exact percentage splits\.

## Properties<a name="disconnect-hang-up-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/distribute-by-percentage-properties.png)

## Configured block<a name="disconnect-hang-up-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/distribute-by-percentage-configured.png)

## Sample flows<a name="disconnect-hang-up-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample AB Test](sample-ab-test.md)