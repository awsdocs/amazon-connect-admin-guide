# Contact block: Loop<a name="loop"></a>

## Description<a name="loop-description"></a>
+ Counts the number of times customers are looped through the **Looping** branch\.
+ After the loops are completed, the **Complete** branch is followed\. 
+ This block is often used with a **Get customer input** block\. For example, if the customer doesn't succeed in entering their account number, you can loop to give them another opportunity to enter it\. 

## Supported channels<a name="loop-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Contact flow types<a name="loop-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="loop-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/loop-properties.png)

## Configuration tips<a name="loop-tips"></a>
+ If you enter 0 for the loop count, the **Complete** branch is followed the first time this block runs\.

## Configured block<a name="loop-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/loop-configured.png)