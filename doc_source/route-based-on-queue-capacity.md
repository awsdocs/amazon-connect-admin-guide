# Route contacts based on queue capacity<a name="route-based-on-queue-capacity"></a>

To define routing decisions based on queue capacity, use a [Transfer to queue](transfer-to-queue.md) block to check whether a queue is full \([Maximum contacts in queue](set-maximum-queue-limit.md)\), and then route the contact accordingly\.

The [Transfer to queue](transfer-to-queue.md) block checks the [Maximum contacts in queue](set-maximum-queue-limit.md)\. If no limit is set, the queue is limited to the number of total concurrent contacts for the following quotas: 
+ Active tasks per instance
+ Concurrent calls per instance
+ Concurrent chats per instance