# Set the Maximum contacts in queue limit<a name="set-maximum-queue-limit"></a>

You can define routing decisions based on queue capacity\. For example, use a **Transfer to queue** block to check whether a queue is full, and then route the contact accordingly\.

The **Transfer to queue** block checks the maximum capacity limit you set here\. If no limit is set, the queue is limited to the number of concurrent contacts set in the service quota for the instance\.

1. Choose **Routing**, **Queues**, **Add new queue**\. Or, edit an existing queue\.

1. Under **Maximum contacts in queue** choose **Set limit**\.

1. Specify how many contacts can be in the queue before it's considered full\.