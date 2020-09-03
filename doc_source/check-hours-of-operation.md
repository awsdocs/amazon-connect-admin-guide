# Contact block: Check hours of operation<a name="check-hours-of-operation"></a>

## Contact flow types<a name="check-hours-of-operation-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="check-hours-of-operation-description"></a>
+ Checks whether the contact is occurring within or outside of the hours of operation defined for the queue\.
+ Branches based on specified hours of operation\.

## Properties<a name="check-hours-of-operation-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-hours-of-operation-properties.png)

You can set up multiple hours of operation so you have one for various queues\. For instructions, see [Set the hours of operation and timezone for a queue](set-hours-operation.md)\. 

## Configuration tips<a name="check-hours-of-operation-configuration"></a>
+ [Agent queues](concepts-queues-standard-and-agent.md) that are automatically created for each agent in your instance do not include an hours of operation\. 
+ If you use this block to check the hours of operation for an agent queue, the check fails and the contact is routed down the **Error** branch\.

## Configured block<a name="check-hours-of-operation-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-hours-of-operation-configured.png)

## Related topics<a name="check-hours-of-operation-related"></a>
+ [Set the hours of operation and timezone for a queue](set-hours-operation.md)

## Sample flows<a name="check-hours-of-operation-samples"></a>

[Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="check-hours-of-operation-scenarios"></a>

See these topics for scenarios that use this block:
+ [Manage contacts in a queue](queue-to-queue-transfer.md)