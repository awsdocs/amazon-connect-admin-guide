# Create a Routing Profile<a name="routing-profiles"></a>

While queues are a 'waiting area' for contacts, a routing profile links queues to agents\. When you create a routing profile, you specify which queues will be in it\. You can also specify whether one queue should be prioritized over another\. 

Each agent is assigned to one routing profile\. 

**To create a routing profile**

1. Choose **Users**, **Routing profiles**, **Add new profile**\.

1. Enter or choose the following information:
   + **Name**—A searchable display name\. 
   + **Description**—The routing profile's function\.
   + **Routing profile queues**—A queue to associate with the routing profile\. You can add multiple queues\.
   + **Priority**—The order in which contacts are handled by the queue they are in\. Set values in order of importance, with the lowest number equaling the highest priority\. For example, a contact in a queue with a priority of 2 would be a lower priority than a contact in a queue with a priority of 1\.
   + **Delay \(in seconds\)**—The minimum queue time before the contact is routed to an agent with a matching queue/threshold combination\. 
   + **Default outbound queue**—Outbound calls must be associated with one of the associated queues\. 

1. Choose **Add new profile**\.

## Example Routing Profile<a name="example-routing-profile"></a>

The following is an example routing profile\.


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Premium Support 1  |  1  |  0  | 
|  Premium Support 2  |  1  |  0  | 
|  Premium Support 3  |  2  |  20  | 
|  Premium Support 4  |  3  |  80  | 

This profile prioritizes Premium Support 1 and Premium Support 2 equally \(because each has a priority 1\)\.
+ Agents with this profile may take contacts for Premium Support 3 when customers for Premium Support 3 are waiting for 20 seconds or longer \(and no Premium Support 1 or Premium Support 2 contacts are in queue\)\.
+ Agents with this profile may take contacts for Premium Support 4 when customers for Premium Support 4 are waiting 80 seconds or longer \(and no contacts for Premium Support 1, Premium Support 2 or Premium Support 3 are in queue\)\.