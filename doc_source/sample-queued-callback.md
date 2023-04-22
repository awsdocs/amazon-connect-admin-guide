# Sample queued callback<a name="sample-queued-callback"></a>

**Note**  
This sample flow is available in previous Amazon Connect instances\. In new instances, you can see examples of queued callback in [Sample interruptible queue flow with callback](sample-interruptible-queue.md) and [Sample queue configurations](sample-queue-configurations.md)\.

Type: Flow \(inbound\)

This flow provides callback queue logic\. Here's how it works: 

1. After a voice prompt, a working queue is selected and its queue status is checked\.

1. A voice prompt tells the customer if the wait time for the selected queue is longer than 5 minutes\. Customers are offered a choice to wait in the queue or to be placed into a callback queue\. 

1. If the customer decides to wait in the queue, the **Set customer queue flow** block places them in a queue flow that provides a callback option\. That is, it places them in **Sample interruptible queue flow with callback**\. 

1. If the customer chooses to be placed into a callback queue, their number is stored in the **Store customer input** block\. Then their callback number is set, and they are transferred to the callback queue\.

For information about queued callbacks, see the following topics:
+ [](setup-queued-cb.md) 
+ [Flow block: Transfer to queue](transfer-to-queue.md) 
+ [About queued callbacks in metrics](about-queued-callbacks.md) 