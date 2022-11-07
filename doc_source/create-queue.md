# Create a queue<a name="create-queue"></a>

**How many queues can I create?** To view your quota of **Queues per instance**, open the Service Quotas console at [https://console\.aws\.amazon\.com/servicequotas/](https://console.aws.amazon.com/servicequotas/)\.

1. On the navigation menu, choose **Routing**, **Queues**, **Add new queue**\.

1. Add the appropriate information about your queue and choose **Add new queue**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/add-a-new-queue.png)

   See the following topics for detailed information about each of the above areas:

   1. [Set the hours of operation and timezone for a queue](set-hours-operation.md)

   1. [Set up outbound caller ID](queues-callerid.md)

   1. [Set the Maximum contacts in queue limit](set-maximum-queue-limit.md)

   1. [Create quick connects](quick-connects.md)

   The queue is automatically active\.

1. Assign the queue to a routing profile; for information, see [Create a routing profile](routing-profiles.md)\. The routing profile links the queue and agents together\.

To learn how queues work, see [Routing profiles](concepts-routing.md) and [Queue\-based routing](concepts-queue-based-routing.md)\.