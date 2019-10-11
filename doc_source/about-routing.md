# How Routing Works<a name="about-routing"></a>

Contacts are routed through your contact center based on the routing logic you define in your contact flows\. You can also use routing profiles to manage how agents are allocated to queues, such as routing specific types of contacts to agents with specific skill sets\. If no agent with the required skill set is available, the contact is placed in the queue you define in the contact flow\.

Contacts in a queue are automatically prioritized and forwarded to the next available agent\. Customers are placed on hold if there are no available agents\. The order in which they are serviced is determined by their time in queue, on a first\-come, first\-served basis\. If multiple agents are available, the contact is routed to the agent who has been in the **Available** status for the longest time\.

A routing profile may assign a priority to one queue over another, but the priority within the queue is always set by the order the contact was added to the queue\.

Use the metrics and reporting features of Amazon Connect to monitor queue performance and wait times in your in your contact center to optimize agent efficiency and reduce customer hold times\. Make sure to plan for peak busy times and how additional contacts are handled when your contact center is at full capacity\. To learn more about queue metrics, see [Amazon Connect Metrics and Contact Trace Records](amazon-connect-metrics.md)\. To learn more about using queue metric attributes in contact flows, see [How to Use System Metric Attributes](attrib-system-metrics.md)\.

Queue metrics can be monitored and reviewed using both real\-time and historical metrics\.