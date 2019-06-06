# Amazon Connect Queues<a name="connect-queues"></a>

A queue is 'waiting area' that holds contacts to be answered by agents\. You can use a single queue to handle all incoming contacts, or you can set up queues mapped to agents with specific skill sets\. 

Contacts are routed through your contact center based on the routing logic you define in your contact flows\. You can also use routing profiles to manage how agents are allocated to queues, such as routing specific types of contacts to agents with specific skill sets\. If no agent with the required skill set is available, the contact is placed in the queue you define in the contact flow\.

Calls in a queue are automatically prioritized and forwarded to the next available agent\. Customers are placed on hold if there are no available agents\. The order in which they are serviced is determined by their time in queue, on a first\-come, first\-served basis\. If multiple agents are available, the call is routed to the agent who has been in the **Available** status for the longest time\.

A routing profile may assign a priority to one queue over another, but the priority within the queue is always set by the order the contact was added to the queue\.

Use the metrics and reporting features of Amazon Connect to monitor queue performance and wait times in your in your contact center to optimize agent efficiency and reduce customer hold times\. Make sure to plan for peak busy times and how additional calls are handled when your contact center is at full call capacity\. To learn more about queue metrics, see [Amazon Connect Metrics and Contact Trace Records](amazon-connect-metrics.md)\. To learn more about using queue metric attributes in contact flows, see [Using System Metric Attributes](connect-contact-attributes.md#attrib-system-metrics)\.

Queue metrics can be monitored and reviewed using both real\-time and historical metrics\.

## Set the Hours of Operation<a name="set-hours-operation"></a>

Hours of operation define when a queue is available, and may be referenced in contact flows\. Hours of operation are a required component when setting up queues, and must be completed first\.

**To add hours of operation in the console**

1. Choose **Routing**, **Hours of operation**\.

1. To create a template, choose **Add new hours** and enter a name and a description\.

1. For **Time zone**, select a value\.

1. For **Add new**, set new hours\.

1. Choose **Save**\.

## Create a Queue<a name="create-queue"></a>

When you create a queue, it is automatically active and can be assigned to a routing profile\. Users with the proper permissions can deactivate the queue, which puts it in an offline mode and makes it unavailable to assign to a routing profile\.

When you create a queue, you can specify an **Outbound caller ID name** and **Outbound caller ID number**\. You can also provide a phone number in a **Set callback number** block in a contact flow\. The callback name and number is sent as the origination party when Amazon Connect initiates the call to the destination\. However, the information displayed to the person called may not always match the name or number set during call initiation\. In some cases, the callback name is provided by the carrier of the person you are calling\. The information may not be up\-to\-date with that carrier, or the number may get passed differently between systems due to hardware or configuration differences\. If this is the case, the person that you call may not see the phone number, or may see the name of a previously registered owner of the number, instead of the name of the registered person from your organization\.

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

## Create a Routing Profile<a name="routing-profiles"></a>

A routing profile is a collection of queues that determines how contacts are routed to agents\. Routing profiles are used to prioritize contacts across specific queues and manage the priority in which contacts are handled based on the queues they are routed to\. Routing profiles are managed and assigned to agents by the administrator\. An agent can only be assigned a single routing profile at a time; however, they may serve multiple queues, based on rules defined in the routing profile\.

**To create a routing profile**

1. Choose **Users**, **Routing profiles**, **Add new profile**\.

1. Enter or choose the following information:
   + **Name**—A searchable display name\. 
   + **Description**—The routing profile's function\.
   + **Routing profile queues**—A queue to associate with the routing profile\. You can add multiple queues\.
   + **Priority**—The order in which contacts are handled by the queue they are in\. Set values in order of importance, with the lowest number equaling the highest priority\. For example, a contact in a queue with a priority of 2 would be a lower priority than a contact in a queue with a priority of 1\.
   + **Delay \(in seconds\)**—The minimum queue time before the call is routed to an agent with a matching queue/threshold combination\. 
   + **Default outbound queue**—Outbound calls must be associated with one of the associated queues\. 

1. Choose **Add new profile**\.

### Example Routing Profile<a name="example-routing-profile"></a>

The following is an example routing profile\.


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Premium Support 1  |  1  |  0  | 
|  Premium Support 2  |  1  |  0  | 
|  Premium Support 3  |  2  |  20  | 
|  Premium Support 4  |  3  |  80  | 

This profile prioritizes Premium Support 1 and Premium Support 2 equally \(because each has a priority 1\)\.
+ Agents with this profile may take calls for Premium Support 3 when customers for Premium Support 3 are waiting for 20 seconds or longer \(and no Premium Support 1 or Premium Support 2 calls are in queue\)\.
+ Agents with this profile may take calls for Premium Support 4 when customers for Premium Support 4 are waiting 80 seconds or longer \(and no calls for Premium Support 1, Premium Support 2 or Premium Support 3 are in queue\)\.