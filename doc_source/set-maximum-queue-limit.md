# Set the Maximum contacts in queue limit<a name="set-maximum-queue-limit"></a>

To determine how many contacts can be in a [standard queue](concepts-queues-standard-and-agent.md) at the same time, you set the **Maximum contacts in queue** limit for the standard queue\. This setting does not apply to [agent queues](concepts-queues-standard-and-agent.md); those are always limited to 10 contacts\. 

This setting applies to all the contacts that are in the standard queue, across all channels\. For example, you set **Maximum contacts in queue** to 100 and configure the queue for calls, chats, and tasks\. This means the limit is set to a total of 100 concurrent calls AND chats AND active tasks in the queue\. 

**Important**  
By default you cannot set **Maximum contacts in queue** to be greater than your **Concurrent calls per instance** service quota\.  
For information about default service quotas and how to request an increase, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

**To set Maximum contacts in queue**

1. On the navigation menu, choose **Routing**, **Queues**, **Add new queue**\. Or, edit an existing queue\.

1. Under **Maximum contacts in queue** choose **Set limit**\.

1. Specify how many contacts can be in the queue before it's considered full\.

   Queued callbacks count towards the queue size limit, but they are routed to the error branch\. For example, if you have a queue that handles both callbacks and incoming calls, and that queue reaches the size limit:
   + The next callback is routed to the error branch\.
   + The next incoming call gets a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/maximum-contacts-in-queue.png)