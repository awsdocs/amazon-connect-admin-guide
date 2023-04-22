# Create a queue<a name="create-queue"></a>

This topic explains how to create a queue using the Amazon Connect console\. To create queues programmatically, see the [create\-queue](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/connect/create-queue.html) AWS CLI or [CreateQueue](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateQueue.html) in the *Amazon Connect API Reference*\.

**How many queues can I create?** To view your quota of **Queues per instance**, open the Service Quotas console at [https://console\.aws\.amazon\.com/servicequotas/](https://console.aws.amazon.com/servicequotas/)\.

**To create a queue**

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.\. Use an **Admin** account, or an account that has **Routing \- Create queues** security profile permissions\.

1. In Amazon Connect, on the navigation menu, choose **Routing**, **Queues**, **Add new queue**\.

1. Add the appropriate information about your queue and choose **Add new queue**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/add-a-new-queue.png)

   See the following topics for detailed information about each of the above areas:

   1. [Set the hours of operation and timezone for a queue](set-hours-operation.md)

   1. [Set up outbound caller ID](queues-callerid.md)

   1. [Set the Maximum contacts in queue limit](set-maximum-queue-limit.md)

   1. [Create quick connects](quick-connects.md)

   The queue is automatically active\.

1. Assign the queue to a routing profile; for information, see [Create a routing profile](routing-profiles.md)\. The routing profile links the queue and agents together\.

1. Add Tags to identify, organize, search for, filter and control who can access this queue\. For more information, see [Tagging resources in Amazon Connect](tagging.md)\.

To learn how queues work, see [Concepts: Routing profiles](concepts-routing.md) and [Concepts: Queue\-based routing](concepts-queue-based-routing.md)\.