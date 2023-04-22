# Flow block: Check hours of operation<a name="check-hours-of-operation"></a>

## Description<a name="check-hours-of-operation-description"></a>
+ Checks whether the contact is occurring within or outside of the hours of operation defined for the queue\.
+ Branches based on specified hours of operation\.

## Supported channels<a name="check-hours-of-operation-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="check-hours-of-operation-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="check-hours-of-operation-properties"></a>

The following image shows the **Properties** page of the **Check hours of operation** block\. The block is configured for specific hours of operation\.

![\[The properties page of the Check hours of operation block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-hours-of-operation-properties.png)

You can set up multiple hours of operation so you have one for various queues\. For instructions, see [Set the hours of operation and timezone for a queue](set-hours-operation.md)\. 

## Configuration tips<a name="check-hours-of-operation-configuration"></a>
+ [Agent queues](concepts-queues-standard-and-agent.md) that are automatically created for each agent in your instance do not include an hours of operation\. 
+ If you use this block to check the hours of operation for an agent queue, the check fails and the contact is routed down the **Error** branch\.

## Configured block<a name="check-hours-of-operation-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It is configured for **Basic Hours** of operation\. It has three branches: **In hours**, **Out of Hours**, and **Error**\. 

![\[A configured Check hours of operation block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-hours-of-operation-configured.png)

## Related topics<a name="check-hours-of-operation-related"></a>
+ [Set the hours of operation and timezone for a queue](set-hours-operation.md)

## Sample flows<a name="check-hours-of-operation-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.

[Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="check-hours-of-operation-scenarios"></a>

See these topics for scenarios that use this block:
+ [Manage contacts in a queue](queue-to-queue-transfer.md)