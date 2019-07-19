# Real\-time Metrics Definitions<a name="real-time-metrics-definitions"></a>

The following metrics are available to include in real\-time metrics reports in Amazon Connect\. The metrics available to include in a report depend on the report type\.

**Abandoned**  <a name="abandoned-real-time"></a>
Count of contacts disconnected by the customer while in the queue during the specified time range\. Contacts queued for callback are not counted as abandoned\.

**Active**  <a name="active-real-time"></a>
Indicates whether the agent is currently active on a contact\. The value is 1 \(true\) or 0 \(false\)\.

**ACW**  <a name="aftercallwork-real-time"></a>
Count of agents with a status of **AfterCallWork**\.

**Agent First Name **  <a name="agent-first-name-real-time"></a>
The first name of the agent, as entered in their Amazon Connect user account\.

**Agent Hierarchy**  <a name="agent-hierarchy-real-time"></a>
The hierarchy the agent is assigned to, if any\.

**Agent hung up**  <a name="agent-hung-up-real-time"></a>
Count of contacts disconnected where the agent disconnected before the customer\.

**Agent Last Name**  <a name="agent-last-name-real-time"></a>
The last name of the agent, as entered in their Amazon Connect user account\.

**Agent Name**  <a name="agent-name-real-time"></a>
The name of the agent, displayed as follows: **Agent Last Name**, **Agent First Name**\.

**AHT**  <a name="average-handled-time-real-time"></a>
Average time, from start to finish, that a contact was connected with an agent \(average handled time\)\. This is calculated by averaging the amount of time between the contact being answered by an agent and the contact ending\.

**API contacts handled**  <a name="api-contacts-handled-real-time"></a>
Count of contacts that were initiated by an API operation, such as `StartOutboundVoiceContact`, and handled by an agent\.

**Availability**  <a name="availability-real-time"></a>
Indicates whether the agent is currently in the **Available** status\. The value is 1 \(true\) or 0 \(false\)\.

**Available**  <a name="available-real-time"></a>
Count of agents with a status of **Available**\.

**Avg abandon time**  <a name="average-abandon-time-real-time"></a>
Average time, in seconds, that abandoned contacts were in the queue before being abandoned\.

**Avg ACW**  <a name="average-aftercallwork-real-time"></a>
Average time, in seconds, that an agent spent in the **AfterCallWork** status during the specified time range\.

**Avg hold time**  <a name="average-hold-time-real-time"></a>
Average time, in seconds, that a contact in the queue was on hold\.

**Avg interaction time**  <a name="average-interaction-time-real-time"></a>
Average time, in seconds, that contacts were connected to and interacting with agents\. This does not include hold time or time spent waiting in the queue\.

**Avg interaction and hold time**  <a name="average-interaction-hold-time-real-time"></a>
Average time, in seconds, that contacts in the queue spent interacting with agents and on hold\. This is calculated as follows:  
Avg hold time \+ Avg interaction time

**Avg queue answer time**  <a name="average-queue-answer-time-real-time"></a>
Average time, in seconds, that a contact was in the queue before being answered by an agent\. This is calculated using the amount of time that the contact was in the queue, not any time that the contact spent in prior steps of the contact flow, such as listening or responding to prompts\.

**Callback contacts handled**  <a name="callback-contacts-handled-real-time"></a>
Count of contacts handled by an agent that were queued callbacks\.

**Consult**  <a name="consult-real-time"></a>
Count of contacts in the queue that were handled by an agent, and the agent consulted with another agent or a call center manager during the contact\.

**Contact State**  <a name="contact-state-real-time"></a>
The state of the most recent contact the agent handled\.

**Duration**  <a name="duration-real-time"></a>
Amount of time that the agent has been in the current status\.

**Error**  <a name="error-real-time"></a>
Count of agents with a status of **Error**\.

**Handled**  <a name="handled-real-time"></a>
Count of contacts in the queue that were answered by an agent\.

**Handled in**  <a name="handled-in-real-time"></a>
Count of incoming contacts handled by an agent during the specified time range that were initiated using one of the following methods: inbound call, transfer to agent, transfer to queue, or queue\-to\-queue transfer\.

**Handled out**  <a name="handled-out-real-time"></a>
Count of contacts handled by an agent during the specified time range that were initiated by an agent placing an outbound call using the CCP\.

**Hold abandons**  <a name="hold-abandons-real-time"></a>
Count of contacts that disconnected while the customer was on hold\. A disconnect could be because the customer hung up while on hold, or that there was a technical issue with the contact while on hold\.

**In queue**  <a name="in-queue-real-time"></a>
Count of contacts currently in the queue\.

**Max Queued**  <a name="max-queued-real-time"></a>
The longest time that a contact spent waiting in the queue\. This includes all contacts added to the queue, even if they were not connected with an agent, such as abandoned contacts\.

**Missed**  <a name="missed-real-time"></a>
Count of contacts routed to an agent but not answered by the agent, including contacts abandoned by the customer, during the specified time range\. A contact can be counted as missed multiple times, once for each time it is routed to an agent but not answered\.

**NPT**  <a name="non-productive-time-real-time"></a>
\(Non\-Productive Time\) Count of agents in a custom status \(any status other than **Available**, **Error**, or **Offline**\.\) Agents can handle contacts while in a custom status\.

**Occupancy**  <a name="occupancy-real-time"></a>
Percentage of time the agent was active on contacts during the specified time range\.

**Oldest**  <a name="oldest-real-time"></a>
Length of time in the queue for the contact that has been in the queue the longest\.

**On call**  <a name="on-call-real-time"></a>
Count of agents currently on a contact\.

**Online**  <a name="online-real-time"></a>
Count of agents with a status other than **Offline**\.

**Queue**  <a name="queue-real-time"></a>
The name of the queue associated with the most recent contact the agent handled\.

**Queued**  <a name="queued-real-time"></a>
Count of contacts added to the queue during the specified time range\.

**Routing Profile**  <a name="routing-profile-real-time"></a>
The routing profile for the agent\.

**Scheduled**  <a name="scheduled-real-time"></a>
Count of customers in the queue for which there is a callback scheduled\.

**SL *X***  <a name="service-level-real-time"></a>
Percentage of contacts removed from the queue between 0 and *X* seconds after being added to it \(Service Level\)\. A contact is removed from the queue when one of the following occurs: an agent answers the call, the customer abandons the call, or the customer requests a call back\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\.

**Staffed**  <a name="staffed-real-time"></a>
Count of agents logged in and with a status of **Available**, **On call**, or **ACW**\.

**Status**  <a name="status-real-time"></a>
The current status of the agent\. Possible values include **Available** and **AfterCallWork**\.

**Transferred in**  <a name="transferred-in-real-time"></a>
Count of contacts transferred into the queue during the specified time range\.

**Transferred in from queue**  <a name="transferred-in-from-queue-real-time"></a>
Count of contacts transferred into the queue from another queue during a **Customer queue flow**\.

**Transferred out**  <a name="transferred-out-real-time"></a>
Count of contacts transferred out of the queue during the specified time range\.

**Transferred out from queue**  <a name="transferred-out-from-queue-real-time"></a>
Count of contacts transferred out of the queue to another queue during a **Customer queue flow**\.