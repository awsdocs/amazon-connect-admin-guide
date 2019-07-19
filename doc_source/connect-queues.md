# Create Amazon Connect Queues<a name="connect-queues"></a>

A queue is 'waiting area' that holds contacts to be answered by agents\. You can use a single queue to handle all incoming contacts, or you can set up queues mapped to agents with specific skill sets\. 

Contacts are routed through your contact center based on the routing logic you define in your contact flows\. You can also use routing profiles to manage how agents are allocated to queues, such as routing specific types of contacts to agents with specific skill sets\. If no agent with the required skill set is available, the contact is placed in the queue you define in the contact flow\.

Contacts in a queue are automatically prioritized and forwarded to the next available agent\. Customers are placed on hold if there are no available agents\. The order in which they are serviced is determined by their time in queue, on a first\-come, first\-served basis\. If multiple agents are available, the contact is routed to the agent who has been in the **Available** status for the longest time\.

A routing profile may assign a priority to one queue over another, but the priority within the queue is always set by the order the contact was added to the queue\.

Use the metrics and reporting features of Amazon Connect to monitor queue performance and wait times in your in your contact center to optimize agent efficiency and reduce customer hold times\. Make sure to plan for peak busy times and how additional contacts are handled when your contact center is at full capacity\. To learn more about queue metrics, see [Amazon Connect Metrics and Contact Trace Records](amazon-connect-metrics.md)\. To learn more about using queue metric attributes in contact flows, see [Using System Metric Attributes](connect-contact-attributes.md#attrib-system-metrics)\.

Queue metrics can be monitored and reviewed using both real\-time and historical metrics\.

## Create a Queue<a name="create-queue"></a>

When you create a queue, it is automatically active and can be assigned to a routing profile\. Users with the proper permissions can deactivate the queue, which puts it in an offline mode and makes it unavailable to assign to a routing profile\.

**To create a queue**

1. Choose **Routing**, **Queues**, **Add new queue**\.

1. Add the appropriate information about your queue and choose **Add new queue**\.

**To edit a queue**

1. Choose **Routing**, **Queues**, and select the queue to edit\.

1. Edit the queue details as required\.

1. Choose **Save**\.

**To disable an active queue**

1. Choose **Routing**, **Queues**\.

1. Hover over the name of the queue to edit and choose the power icon\.

1. Choose **Disable**\.