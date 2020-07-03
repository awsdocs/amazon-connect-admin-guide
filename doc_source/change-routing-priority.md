# Contact Block: Change Routing Priority / Age<a name="change-routing-priority"></a>

## Contact flow types<a name="change-routing-priority-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Outbound Whisper flow
+ Inbound contact flow
+ Customer queue flow
+ Create Outbound Whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="change-routing-priority-description"></a>
+ Change a customer's position in the queue\.

## Properties<a name="change-routing-priority-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/change-routing-priority-properties.png)

This block gives you two options for changing a customer's position in queue: 
+ **Set priority**\. The default priority for new contacts is 5\. You can raise the priority of a contact \- compared to other contacts in the queue \- by assigning them a higher priority, such as 1 or 2\. 
+ **Adjust by time**\. You can add or subtract seconds or minutes from the amount of time the current contact spends in queue\. Contacts are routed to agents on a first\-come, first\-served basis\. So changing their amount of time in queue compared to others also changes their position in queue\.

Here's how this block works:

1. Amazon Connect takes the actual “time in queue” for the contact \(in this case, how long this specific contact has spent in queue so far\), and adds the number of seconds you specified in the **Adjust by time** property\.

1. The additional seconds makes this specific contact look artificially older than it is\. 

1. The routing system now perceives this contact’s “time in queue” as longer than it actually is, which affects its position within the ranked list\.

## Configured block<a name="change-routing-priority-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/change-routing-priority-configured.png)

## Sample flows<a name="change-routing-priority-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample customer queue priority](sample-customer-queue-priority.md)
+  [Sample queue configurations](sample-queue-configurations.md)

## Scenarios<a name="change-routing-priority-scenarios"></a>

See these topics for more information about how routing priority works:
+ [Routing profiles](concepts-routing.md)
+ [How routing works](about-routing.md)