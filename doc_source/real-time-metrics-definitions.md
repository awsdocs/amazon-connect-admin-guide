# Real\-time metrics definitions<a name="real-time-metrics-definitions"></a>

The following metrics are available to include in real\-time metrics reports in Amazon Connect\. The metrics available to include in a report depend on the report type\.

**Tip**  
Developers can use the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API to get a subset of the following real\-time metrics from the specified Amazon Connect instance\.

## Abandoned<a name="abandoned-real-time"></a>

Count of contacts disconnected by the customer while in the queue during the specified time range\. Contacts queued for callback are not counted as abandoned\. When you create a customized real\-time metrics report, to include this metric, choose a **Queues** report for the type\. On the **Filters** tab, choose **Queues**, then on the **Metrics** tab you'll have the option to include **Abandoned**\. 

## Active<a name="active-real-time"></a>

Count of active slots\. This number is incremented for each contact where the contact state is either Connected, On Hold, After contact work, or Outbound ring\.

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `SLOTS_ACTIVE`\.

## ACW<a name="aftercallwork-real-time"></a>

Count of contacts who are in an **AfterContactWork** state\. \(After contact work is also known as After call work\.\)  After a conversation between an agent and customer ends, the contact is moved into the ACW state\.

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_AFTER_CONTACT_WORK`\. The name of this metric is confusing because in the Amazon Connect console, ACW counts the number of *contacts* who are in an ACW state, not the number of agents\. 

To learn more about agent status and contact states, see [About agent status](metrics-agent-status.md) and [About contact states](about-contact-states.md)\.

## Agent Activity<a name="agent-activity-state-real-time"></a>

If an agent is handling a single contact, this metric may have the following values: Available, Incoming, On contact, Rejected, Missed, Error, After contact work, or a custom status\. 

If an agent is handling concurrent contacts, Amazon Connect uses the following logic to determine the state: 
+ If at least one contact is in Error, Agent Activity = Error\.
+ Else if at least one contact is Missed contact, Agent Activity = Missed\.
+ Else if at least one contact is Rejected contact, Agent Activity = Rejected\.
+ Else if at least one contact is Connected, On Hold, or Outbound contact/Outbound callback, Agent Activity = On contact\.
+ Else if at least one contact is After contact work, Agent Activity = After Contact Work\.
+ Else if at least one contact is Incoming/Inbound Callback, Agent Activity = Incoming\.
+ Else if agent status is a custom status, Agent Activity is the custom status\.
+ Else if agent status is Available, Agent Activity = Available\.

If a supervisor is using the Manager Monitor feature to monitor a particular agent as they interact with a customer, then the supervisor’s Agent Activity will display as Monitoring\. The Agent Activity of the agent who is being monitored is still On Contact\.

## Agent First Name<a name="agent-first-name-real-time"></a>

The first name of the agent, as entered in their Amazon Connect user account\.

## Agent Hierarchy<a name="agent-hierarchy-real-time"></a>

The hierarchy the agent is assigned to, if any\.

## Agent hung up<a name="agent-hung-up-real-time"></a>

Count of contacts disconnected where the agent disconnected before the customer\.

## Agent Last Name<a name="agent-last-name-real-time"></a>

The last name of the agent, as entered in their Amazon Connect user account\.

## Agent Name<a name="agent-name-real-time"></a>

The name of the agent, displayed as follows: **Agent Last Name**, **Agent First Name**\.

## Agent non\-response<a name="agent-non-response-real-time"></a>

Count of contacts routed to an agent but not answered by that agent, including contacts abandoned by the customer\. 

If a contact is not answered by a given agent, we attempt to route it to another agent to handle; the contact is not dropped\. Because a single contact can be missed multiple times \(including by the same agent\), it can be counted multiple times: once for each time it is routed to an agent but not answered\.

This metric was previously named **Missed**\.

## AHT \(Average Handled Time\)<a name="average-handled-time-real-time"></a>

The average time, from start to finish, that a contact was connected with an agent \(average handled time\)\. It includes talk time, hold time, and After Contact Work \(ACW\) time\.

AHT is calculated by averaging **the amount of time between the contact being answered by an agent** and **the completion of work on that contact by an agent**\.

## API contacts handled<a name="api-contacts-handled-real-time"></a>

Count of contacts that were initiated by an API operation, such as `StartOutboundVoiceContact`, and handled by an agent\.

## Availability<a name="availability-real-time"></a>

For each agent, the number of available slots they have that can be routed contacts\. 

The number of available slots for an agent are based on their [routing profile](routing-profiles.md)\. For example, let's say an agent's routing profile specifies they can handle either one voice contact **or** up to three chat contacts simultaneously\. If they are currently handling one chat, they have two available slots left, not three\.

What causes this number to go down? A slot is considered unavailable when:
+ A contact in the slot is: connected to the agent, in After Contact Work, inbound ringing, outbound ringing, missed, or in an error state\.
+ A contact in the slot is connected to the agent and on hold\.

Amazon Connect doesn't count an agent's slots when:
+ The agent has set their status in the CCP to a custom status, such as Break or Training\. Amazon Connect doesn't count these slots because agents can't take inbound contacts when they've set their status to a custom status\. 
+ The agent can't take contacts from that channel per their routing profile\. 

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `SLOTS_AVAILABLE`\.

## Available<a name="available-real-time"></a>

The number of agents who can take an inbound contact\. An agent can only take inbound contacts when they manually set their status to Available in the CCP \(or in some cases when their supervisor changes it\)\.

This is different from how many more inbound contacts an agent could take\. If you want to know how many more contacts an agent can have routed to them, look at the Availability metric\. It indicates how many slots the agent has free\.

What causes this number to go down? An agent is considered **unavailable** when: 
+ The agent has set their status in the CCP to a custom status, such as Break or Training\. Amazon Connect doesn't count these slots because agents can't take inbound contacts when they've set their status to a custom status\. 
+ The agent has at least one contact ongoing\.  
+ The agent has a contact in a missed or error state, which prevents the agent from taking any more contacts until they are flipped back to routable\. 

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_AVAILABLE`\.

## Average API Connecting Time<a name="average-api-connecting-time-real-time"></a>

The average time between when a contact is initiated using an Amazon Connect API, and the agent is connected\.

## Avg abandon time<a name="average-abandon-time-real-time"></a>

Average time, in seconds, that abandoned contacts were in the queue before being abandoned\.

## Avg ACW<a name="average-aftercallwork-real-time"></a>

Average time, in seconds, that contacts spent in the **After contact work** state, during the specified time range\.

This is not the average amount of time agents spent on contacts\. 

To learn more about agent status and contact states, see [About agent status](metrics-agent-status.md) and [About contact states](about-contact-states.md)\.

## Avg callback connecting time<a name="rtm-avg-callback-connecting-time"></a>

Then average time between when callback contacts are initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

No equivalent to this metric is available in the GetCurrentMetricData API\. 

The following image shows the five parts that go into calculating **Avg callback connecting time**\. It also shows what is in the agent event stream\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-agent-callback-connection-time.png)

## Avg hold time<a name="average-hold-time-real-time"></a>

Average time, in seconds, that a contact in the queue was on hold\.

This metric doesn't apply to tasks so you'll notice a value of 0 on the report for them\.

## Avg incoming connecting time<a name="rtm-avg-incoming-connecting-time"></a>

The average time between when contacts are initiated Amazon Connect reserving the agent for the contact, and the agent is connected\. 

In the agent event stream, this time is calculated by averaging the duration between the contact state of STATE\_CHANGE event changes from CONNECTING to CONNECTED/MISSED/ERROR\. 

No equivalent to this metric is available in the GetCurrentMetricData API\. 

The following image shows the three parts that go into calculating **Avg incoming connecting time**\. It also shows what is in the agent event stream\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-agent-inbound-connection-time.png)

## Avg interaction time<a name="average-interaction-time-real-time"></a>

Average time, in seconds, that contacts were connected to and interacting with agents\. This does not include hold time or time spent waiting in the queue\.

## Avg interaction and hold time<a name="average-interaction-hold-time-real-time"></a>

Average time, in seconds, that contacts in the queue spent interacting with agents and on hold\. This is calculated as follows:

Avg hold time \+ Avg interaction time

## Avg queue answer time<a name="average-queue-answer-time-real-time"></a>

Average time, in seconds, that a contact was in the queue before being answered by an agent\. This is calculated using the amount of time that the contact was in the queue, not any time that the contact spent in prior steps of the contact flow, such as listening or responding to prompts\.

## Avg outbound connecting time<a name="rtm-avg-outbound-connecting-time"></a>

The average time between when outbound contacts are initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

No equivalent to this metric is available in the GetCurrentMetricData API\. 

The following image shows the four parts that go into calculating **Avg outbound connecting time**\. It also shows what is in the agent event stream\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-agent-outbound-connection-time.png)

## Callback contacts handled<a name="callback-contacts-handled-real-time"></a>

Count of contacts handled by an agent that were queued callbacks\.

## Capacity<a name="capacity-real-time"></a>

Displays the maximum capacity that's set in the routing profile currently assigned to the agent\. This column can be filtered by channel\. 

If an agent's routing profile is configured to handle either one voice **or** up to three chats, then their maximum capacity equals three, when not filtered by channel\.

## Consult<a name="consult-real-time"></a>

Deprecated May 2019\. When used in a report, it returns a dash \(\-\)\. 

Count of contacts in the queue that were handled by an agent, and the agent consulted with another agent or a call center manager during the contact\.

## Contact State<a name="contact-state-real-time"></a>

The state of the contacts the agent is currently handling\. The state can be: **Connected**, **On Hold**, **After contact work**, **Incoming**, **Calling**, or **Missed contact**\. 

For queued callbacks, the contact state can also **Callback incoming** or **Callback dialing**\. 

If a supervisor is using the Manager Monitor feature to monitor a particular agent as they interact with a customer, the supervisor’s contact state is Monitoring; the agent’s contact state is Connected\.

## Duration<a name="duration-real-time"></a>

Amount of time that the agent has been in the current Agent Activity State\.

## Error<a name="error-real-time"></a>

A count of agents in Error state\. An agent is included in this metric if they miss a call or reject a chat/task \(most common\)\. They could also be counted if there is a connection failure\. 

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_ERROR`\.

## Handled<a name="handled-real-time"></a>

Count of contacts in the queue that were answered by an agent\.

## Handled in<a name="handled-in-real-time"></a>

Count of incoming contacts handled by an agent during the specified time range that were initiated using one of the following methods: inbound call, transfer to agent, transfer to queue, or queue\-to\-queue transfer\.

## Handled out<a name="handled-out-real-time"></a>

Count of contacts handled by an agent during the specified time range that were initiated by an agent placing an outbound call using the CCP\.

## Hold abandons<a name="hold-abandons-real-time"></a>

Count of contacts that disconnected while the customer was on hold\. A disconnect could be because the customer hung up while on hold, or that there was a technical issue with the contact while on hold\.

## In queue<a name="in-queue-real-time"></a>

Count of contacts currently in the queue\.

To learn how this is different from Scheduled contacts in a callback scenario, see [How Initial delay affects Scheduled and In queue metrics](scheduled-vs-inqueue.md)\. 

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `CONTACTS_IN_QUEUE`\.

## Max queued<a name="max-queued-real-time"></a>

The longest time that a contact spent waiting in the queue\. This includes all contacts added to the queue, even if they were not connected with an agent, such as abandoned contacts\.

## NPT \(Non\-Productive Time\)<a name="non-productive-time-real-time"></a>

Count of agents who have set their status in the CCP to a custom status\. That is, their CCP status is other than **Available** or **Offline**\.

**Tip**  
Although agents aren't routed any *new inbound* contacts while their CCP status is set to a custom status, it's possible for them to change their CCP status to a custom status while still handling a contact\. For example, let's say an agent is being routed contacts very quickly\. To go on break, they set their status to **Break** proactively, while still finishing up the last contact\. This allows them to go on break and avoid accidentally missing a contact that's routed to them in the sliver of time between the last contact ending and setting their status to Break\.   
Because agents can be **On call** or doing **ACW**, for example, while their CCP is set to a custom status, this means it's possible for agents to be counted as **On call** and **NPT** at the same time\.

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_NON_PRODUCTIVE`\.

## Occupancy<a name="occupancy-real-time"></a>

Percentage of time that an agent was active on contacts\. This percentage is calculated as follows:

\(Agent on contact \(wall clock time\) / \(Agent on contact \(wall clock time\) \+ Agent idle time\)\) 

Where: 
+ \(Agent on contact \+ Agent idle time\) = total amount of agent time
+ So \(Agent on contact\)/\(total amount of agent time\) = percentage of time agents were active on contacts\.

**Important**  
**Occupancy** doesn't account for concurrency\. That is, an agent is considered 100% occupied for a given interval if they are handling at least one contact for that entire duration\. 

## Oldest<a name="oldest-real-time"></a>

Length of time in the queue for the contact that has been in the queue the longest\.

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `OLDEST_CONTACT_AGE`\.

## On contact<a name="on-call-real-time"></a>

Count of agents currently on a contact\. An agent is "on a contact" when they are handling at least one contact who is either connected, on hold, in After contact work, or outbound ring\.

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_ON_CONTACT`\. This metric used to be named On call\. You can still use `AGENTS_ON_CALL` to retrieve data for this metric\.

## Online<a name="online-real-time"></a>

Count of agents who have set their status in the CCP to something other than **Offline**\. For example, they may have set their status to Available, or to a custom value such as Break or Training\.

The Online metric doesn't tell you how many agents can be routed contacts\. For that metric, see [Available](#available-real-time)\. 

This metric can be confusing so let's look at an example\. Say you see this in a Queues report: 
+ Online = 30
+ On Call = 1
+ NPT = 30
+ ACW = 0
+ Error = 0
+ Available = 0

This means 30 agents have set their status in the CCP to a custom status\. 1 of those 30 agents is currently on a contact\.

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_ONLINE`\.

## Queue<a name="queue-real-time"></a>

The name of the queue associated with the contact the agent is currently handling\.

## Queued<a name="queued-real-time"></a>

Count of contacts added to the queue during the specified time range\.

## Routing Profile<a name="routing-profile-real-time"></a>

The routing profile for the agent\.

## Scheduled<a name="scheduled-real-time"></a>

Count of customers in the queue for which there is a callback scheduled\.

To learn how this is different from In queue contacts in a callback scenario, see [How Initial delay affects Scheduled and In queue metrics](scheduled-vs-inqueue.md)\. 

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `CONTACTS_SCHEDULED`\.

## SL *X*<a name="service-level-real-time"></a>

Percentage of contacts removed from the queue between 0 and *X* after being added to it \(Service Level\)\. A contact is removed from the queue when one of the following occurs: an agent answers the call, the customer abandons the call, or the customer requests a call back\. 

For X, you can can choose from pre\-set times in seconds: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\.

### Custom service levels<a name="custom-service-level-real-time"></a>

You can also create custom service level metrics\. You can also choose from additional durations, such as minutes, hours, or days\.

You can add up to 10 custom service levels per report\.

The maximum duration for a custom service level is 7 days\. That's because in Amazon Connect you can't have a contact that goes longer than 7 days\. 

## Staffed<a name="staffed-real-time"></a>

Count of agents who are online in the CCP, and not in NPT \(a custom status\)\. 

Another way of thinking about this is, there are two scenarios in which **Staffed** is not incremented: 
+ The agent's status in the CCP is set to **Offline**\. 
+ The agent's status in the CCP is set to a custom status\. 

For example, let's say an agent sets their status in the CCP to a custom status such as Break and they make an outbound call\. Now the agent is **On call**, but **Staffed** is 0\. 

If the agent sets their status in the CCP to **Available** and makes an outbound call, the agent is **On call** and **Staffed **is 1\. 

 This metric is available on the Queues report\. 

In the [GetCurrentMetricData ](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, this metric is `AGENTS_STAFFED`\.

## Transferred in<a name="transferred-in-real-time"></a>

Count of contacts transferred into the queue during the specified time range\.

## Transferred in from queue<a name="transferred-in-from-queue-real-time"></a>

Count of contacts transferred into the queue from another queue during a **Customer queue flow**\.

## Transferred in by agent<a name="transferred-in-by-agent-real-time"></a>

Count of contacts transferred in by an agent using the CCP\.

## Transferred in from queue<a name="transferred-in-from-queue-real-time"></a>

Count of contacts transferred into the queue from another queue during a **Customer queue flow**\.

## Transferred out<a name="transferred-out-real-time"></a>

Count of contacts transferred out of the queue during the specified time range\.

## Transferred out by agent<a name="transferred-out-by-agent-real-time"></a>

Count of contacts transferred out by an agent using the CCP\.

## Transferred out from queue<a name="transferred-out-from-queue-real-time"></a>

Count of contacts transferred out of the queue to another queue during a **Customer queue flow**\.