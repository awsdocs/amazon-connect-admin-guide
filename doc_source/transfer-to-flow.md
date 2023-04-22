# Flow block: Transfer to flow<a name="transfer-to-flow"></a>

## Description<a name="transfer-to-flow-description"></a>
+ Ends the current flow and transfers the customer to a different flow\.

## Supported channels<a name="transfer-to-flow-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="transfer-to-flow-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="transfer-to-flow-properties"></a>

The following image shows the **Properties** page of the **Transfer to flow** block\. You choose the flow from the dropdown box\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-flow-properties.png)

Only published flows appear in the dropdown list\. 

## Configured block<a name="transfer-to-flow-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has the following branch: **Error**\. 

![\[A configured Transfer to flow block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-flow-configured.png)

1. The contact is routed down the **Error** branch if the flow you have specified to transfer to isn't a valid flow, or it's not a valid flow type \(Inbound, Transfer to Agent, or Transfer to Queue\)\. 

## Sample flows<a name="transfer-to-flow-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample AB test](sample-ab-test.md)

## Scenarios<a name="transfer-to-flow-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up contact transfers](transfer.md)