# Set the Maximum contacts in queue limit<a name="set-maximum-queue-limit"></a>

You can define routing decisions based on queue capacity\. For example, use a **Transfer to queue** block to check whether a queue is full, and then route the contact accordingly\.

The **Transfer to queue** block checks the maximum capacity limit you set here\. If no limit is set, the queue is limited to the number of concurrent contacts set in the service quota for the instance\.

1. On the navigation menu, choose **Routing**, **Queues**, **Add new queue**\. Or, edit an existing queue\.

1. Under **Maximum contacts in queue** choose **Set limit**\.

1. Specify how many contacts can be in the queue before it's considered full\.

   Queued callbacks count towards the queue size limit, but they are routed to the error branch\. For example, if you have a queue that handles both callbacks and incoming calls, and that queue reaches the size limit:
   + The next callback is routed to the error branch\.
   + The next incoming call gets a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.

   For information about service quotas and how to request a change to your queue capacity limit, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/maximum-contacts-in-queue.png)