# Set up routing<a name="connect-queues"></a>

In Amazon Connect, routing consists of three parts: queues, routing profiles, and contact flows\. This topic discusses queues and routing profiles\. For information about contact flows, see [Create Amazon Connect contact flowsCreate contact flows](connect-contact-flows.md)\.

A queue holds contacts waiting to be answered by agents\. You can use a single queue to handle all incoming contacts, or you can set up multiple queues\.

Queues are linked to agents through a routing profile\. When you create a routing profile, you specify: 
+ Which queues will be in it\.
+ Whether one queue should be prioritized over another\.
+ What channels agents will handle in the Contact Control Panel \(CCP\): voice, chat, or both\. 
+ How many chat conversations agents can handle simultaneously, up to 5\.
+ Whether individual queues are for voice, chat, or both\.

Each agent is assigned to one routing profile\.

**Topics**
+ [How routing works](about-routing.md)
+ [Create a queue](create-queue.md)
+ [Disable a queue](disable-a-queue.md)
+ [Set queue capacity](set-maximum-queue-limit.md)
+ [Set the hours of operation](set-hours-operation.md)
+ [Set up outbound caller ID](queues-callerid.md)
+ [Create a routing profile](routing-profiles.md)
+ [Set up queue\-based routing](set-up-queue-based-routing.md)