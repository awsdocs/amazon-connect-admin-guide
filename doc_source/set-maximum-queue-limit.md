# Set the Maximum contacts in queue limit<a name="set-maximum-queue-limit"></a>

By default a queue can contain up to your [service quota](amazon-connect-service-limits.md) for voice, chat, and tasks: 
+ **Concurrent active calls per instance**
+ **Concurrent active chats per instance**
+ **Concurrent active tasks per instance**

To increase one of these quotas, you must request a quota increase\. For more information, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

There may be situations where you want a specific queue to allow fewer contacts than the allowed quota\. For example, if you have a queue that is dedicated to calls about complicated issues that take an average of 15 minutes to resolve, you may want to limit the number of calls allowed in the queue to be less than **Concurrent active calls per instance**\. This prevents customers from waiting for hours\. 

This topic explains how to reduce the allowed number of contacts in a queue for these situations\.

## Reduce the number of contacts allowed in a queue<a name="cap-queue"></a>

To reduce the number of contacts allowed in a [standard queue](concepts-queues-standard-and-agent.md) at the same time, you set the **Maximum contacts in queue** limit for the standard queue\. This setting does not apply to [agent queues](concepts-queues-standard-and-agent.md); those are always limited to 10 contacts\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/maximum-contacts-in-queue2.png)

When you enter a number in **Maximum contacts in queue**, Amazon Connect validates that the number is less than your **Concurrent active calls per instance** service quota\. 

**Important**  
You cannot set **Maximum contacts in queue** to be greater than your **Concurrent calls per instance** service quota\.
If the queue is also used for chats and tasks, they will be subject to the same limit\.
This feature is intended for managing queues that are dedicated to voice calls\.
Incoming calls and queued callbacks count towards the queue size limit\.
For information about default service quotas and how to request an increase, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

**To reduce the number of contacts allowed in a specific queue**

1. On the navigation menu, choose **Routing**, **Queues**, **Add new queue**\. Or, edit an existing queue\.

1. In **Maximum contacts in queue**, choose **Set a limit across all channels**\. If the queue is also used for chats or tasks, then all three channels will be capped at the same maximum\. 

1. In the box, specify how many contacts can be in the queue before it's considered full\. The value cannot exceed the quota for **Concurrent active calls per instance**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/maximum-contacts-in-queue2.png)

## What happens to calls when a queue is full<a name="when-queue-full"></a>
+ Incoming calls: The next incoming call gets a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.
+ Queued callbacks: The next queued callback is routed down the error branch\.

## Queue maximum limit exceptions<a name="max-queue-additional-details"></a>

There are times when you can add more contacts to a queue than the set **Maximum contacts in queue** limit\.
+ There may be a slight delay between the time that a queue reaches its capacity limit and when this limit is enforced in the flow\. This delay could cause incoming contacts to be queued during that time, particularly during bursts of traffic\.

Additionally, Amazon Connect includes a 20 percent buffer to the queue capacity for the following exceptional scenarios:
+ A contact was transformed into a Queued Callback, scheduled to be added to the queue at X time using the **Initial delay** setting in the flow\. However, when the scheduled time arrived, the target queue had reached its **Maximum capacity in queue** limit\. In this scenario, Amazon Connect allows the Queued Callback to be enqueued up to a 20 percent buffer of the **Maximum capacity in queue** limit for the queue\.
+ A contact, previously queued in queue one, is now being transferred to queue two through the flow\. However, when the transfer is attempted, queue two has already reached its **Maximum capacity in queue** limit\. In this scenario, Amazon Connect will allow the transfer to proceed, up to a 20 percent buffer of the **Maximum capacity in queue** limit for queue two\.
+ An agent initiates a manual transfer of a contact into a queue through Quick Connects\. However, when the transfer is attempted, the queue has already reached its **Maximum capacity in queue** limit\. In this scenario, Amazon Connect will allow the transfer to proceed, up to a 20 percent buffer of the **Maximum capacity in queue** limit\.