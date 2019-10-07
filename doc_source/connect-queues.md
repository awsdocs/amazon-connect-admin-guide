# Set Up Routing<a name="connect-queues"></a>

In Amazon Connect routing consists of three parts: queues, routing profiles, and contact flows\. This section covers the first two; for information about contact flows, see [Create Amazon Connect Contact FlowsCreate Contact Flows](connect-contact-flows.md)\.

A queue is 'waiting area' that holds contacts to be answered by agents\. You can use a single queue to handle all incoming contacts, or you can set up multiple queues\.

Queues are linked to agents through a routing profile\. When you create a routing profile, you specify: 
+ Which queues will be in it\.
+ Whether one queue should be prioritized over another\.

Each agent is assigned to one routing profile\.

**Topics**
+ [How Routing Works](about-routing.md)
+ [Create a Queue](create-queue.md)
+ [Set the Hours of Operation](set-hours-operation.md)
+ [Set Up Outbound Caller ID](queues-callerid.md)
+ [Create a Routing Profile](routing-profiles.md)