# Historical Metrics Definitions<a name="historical-metrics-definitions"></a>

The following metrics are available to include in historical metrics reports in Amazon Connect\.

**After contact work time**  <a name="acw-historical"></a>
The total time that an agent spent doing ACW for a contact\.   
You specify the amount of time an agent has to do ACW in their [ agent configuration settings](configure-agents.md)\. When a conversation with a contact ends, the agent is automatically allocated to do ACW for the contact\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Agent answer rate**  <a name="agent-answer-rate-historical"></a>
Percentage of contacts routed to an agent that were answered\.  
Type: String   
Min value: 0\.00%  
Max value: 100\.00%  
Category: Agent activity\-driven metric

**Agent first name**  <a name="agent-first-name-historical"></a>
The first name of the agent, as entered in their Amazon Connect user account\. This metric is available only when grouping by agent\.  
Type: String   
Length: 1\-255

**Agent idle time**  <a name="agent-idle-time-historical"></a>
After the agent sets their status in the CCP to **Available**, this is the amount of time they weren't handling contacts \+ any time their contacts were in an Error state\.   
Agent idle time doesn’t include the amount of time when Amazon Connect starts routing the contact to the agent to when agent picks up or declines the contact\.  
Type: String \(*hh:mm:ss*\)  
Category: Agent activity\-driven metric

**Agent interaction and hold time**  <a name="agent-interaction-hold-time-historical"></a>
Sum of the **Agent interaction time** and **Customer hold time** metrics\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Agent interaction time**  <a name="agent-interaction-time-historical"></a>
Total time that agents spent interacting with customers on a contact\. This does not include hold time or after contact work\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Agent last name**  <a name="agent-last-name-historical"></a>
The last name of the agent, as entered in their Amazon Connect user account\. This metric is available only when grouping by agent\.  
Type: String   
Length: 1\-255

**Agent name**  <a name="agent-name-historical"></a>
The name of the agent, displayed as follows: **Agent last name**, **Agent first name**\. This metric is available only when grouping by agent\.

**Agent non\-response**  <a name="agent-non-response"></a>
Count of contacts routed to an agent but not answered by the agent, including contacts abandoned by the customer\. A contact can be counted as missed multiple times, once for each time it is routed to an agent but not answered\.  
This metric appears as **Contacts missed** in scheduled reports and exported CSV files\.  
Type: Integer   
Category: Agent activity\-driven metric

**Agent on contact time**  <a name="agent-on-contact-time-historical"></a>
Total time that an agent spent on a contact, including hold time and after contact work\. This does not include time spent on a contact while in a custom status\.  
Type: String \(*hh:mm:ss*\)  
Category: Agent activity\-driven metric

**API contacts**  <a name="api-contacts-historical"></a>
Count of contacts that were initiated using an Amazon Connect API operation, such as `StartOutboundVoiceContact`\. This includes contacts that were not handled by an agent\.  
Type: Integer   
Category: CTR\-driven metric

**API contacts handled**  <a name="api-contacts-handled-historical"></a>
Count of contacts that were initiated using an Amazon Connect API operation, such as `StartOutboundVoiceContact`, and handled by an agent\.  
Type: Integer   
Category: CTR\-driven metric

**Average after contact work time**  <a name="average-acw-time-historical"></a>
Average time that an agent spent doing After Contact Work \(ACW\) for their contacts\. This is calculated by averaging `AfterContactWorkDuration` \(from the CTR\) for all contacts included in the report, based on the selected filters\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average agent interaction and customer hold time**  <a name="average-agent-interaction-customer-hold-time-historical"></a>
Average of the sum of the agent interaction and customer hold time\. This is calculated by averaging the sum of the following values from the CTR: `AgentInteractionDuration` and `CustomerHoldDuration`\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average agent interaction time**  <a name="average-agent-interaction-time-historical"></a>
Average time that agents interacted with customers during contacts\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average customer hold time**  <a name="average-customer-hold-time-historical"></a>
Average time that customers spent on hold while connected to an agent\. This is calculated by averaging `CustomerHoldDuration` \(from the CTR\)\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average handle time**  <a name="average-handle-time-historical"></a>
Average time that agents spent on contacts, including hold time and after contact work\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average outbound after contact work time**  <a name="average-outbound-acw-time-historical"></a>
Average time that agents spent doing After Contact Work \(ACW\) after handling an outbound contact\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average outbound agent interaction time**  <a name="average-outbound-agent-interaction-time-historical"></a>
Average time that agents spent interacting with a customer during an outbound contact\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average queue abandon time**  <a name="average-queue-abandon-time-historical"></a>
Average time that contacts waited in the queue before being abandoned\. This is calculated by averaging the difference between `EnqueueTimestamp` and `DequeueTimestamp` \(from the CTR\) for abandoned contacts\. An contact is considered abandoned if it was removed from a queue but not answered by an agent or queued for callback\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Average queue answer time**  <a name="average-queue-answer-time-historical"></a>
Average time that contacts waited in the queue before being answered by an agent\. This is the average of `Duration` \(from the CTR\)\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Callback contacts**  <a name="callback-contacts-historical"></a>
Count of contacts that were initiated from a queued callback\.  
Type: Integer   
Category: CTR\-driven metric

**Callback contacts handled**  <a name="callback-contacts-handled-historical"></a>
Count of contacts that were initiated from a queued callback and handled by an agent\.  
Type: Integer   
Category: CTR\-driven metric

**Contact flow time**  <a name="contact-flow-time-historical"></a>
Total time a contact spent in a contact flow\.  
Outbound contacts don't start in a contact flow, so outbound contacts aren't included\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Contact handle time**  <a name="contact-handle-time-historical"></a>
Total time that an agent spent on contacts, including hold time and **After contact work time**\. This includes any time spent on contacts while in a custom status\.   
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Contacts abandoned**  <a name="contacts-abandoned-historical"></a>
Count of contacts disconnected by the customer while in the queue\. Contacts queued for callback are not counted as abandoned\. When you create customized historical reports, to include this metric, on the **Groupings** tab choose either **Queue** or **Phone Number**\.   
Type: Integer   
Category: CTR\-driven metric

**Contacts abandoned in *X* seconds**  <a name="contacts-abandoned-x-historical"></a>
Count of contacts disconnected by the customer while in the queue for 0 to *X* seconds\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts agent hung up first**  <a name="contacts-agent-hung-up-first-historical"></a>
Count of contacts disconnected where the agent disconnected before the customer\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts answered in *X* seconds**  <a name="contacts-answered-x-historical"></a>
Count of contacts that were answered by an agent between 0 and *X* seconds of being placed in the queue, based on the value of `EnqueueTimestamp`\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts consulted**  <a name="contacts-consulted-historical"></a>
Count of contacts handled by an agent who consulted with another agent in Amazon Connect\. The agent interacts with the other agent, but the customer is not transferred to the other agent\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts handled**  <a name="contacts-handled-historical"></a>
Count of contacts that were connected to an agent\.  
It doesn’t matter how the contact got to the agent\. It could be a customer calling your contact center, or an agent calling the customer\. It could be a contact transferred from one agent to another\. It could be a contact where the agent answered it, but then they weren’t sure what to do and they transferred the contact away again\. As long as the agent was connected to the contact, it increments **Contacts handled**\.   
Type: Integer   
Category: CTR\-driven metric

**Contacts handled incoming**  <a name="contacts-handled-incoming-historical"></a>
Count of incoming contacts that were handled by an agent, including inbound contacts, transferred contacts, and scheduled callbacks\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts handled outbound**  <a name="contacts-handled-outbound-historical"></a>
Count of outbound contacts that were handled by an agent\. This includes contacts that were initiated by an agent using the CCP\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts hold agent disconnect**  <a name="contacts-hold-agent-disconnect-historical"></a>
Count of contacts that were disconnected by the agent while the customer was on hold\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts hold customer disconnect**  <a name="contacts-hold-customer-disconnect-historical"></a>
Count of contacts that were disconnected by the customer while the customer was on hold\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts hold disconnect**  <a name="contacts-hold-disconnect-historical"></a>
Count of contacts disconnected while the customer was on hold\. This includes both contacts disconnected by the agent and contacts disconnected by the customer\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts incoming**  <a name="contacts-incoming-historical"></a>
Count of incoming contacts, including inbound contacts and transferred contacts\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts missed**  <a name="contacts-missed-historical"></a>
Count of contacts routed to an agent but not answered by the agent, including contacts abandoned by the customer\. A contact can be counted as missed multiple times, once for each time it is routed to an agent but not answered\.  
This metric appears as **Agent non\-response** on the **Historical metrics** page in the user interface\.  
Type: Integer   
Category: Agent activity\-driven metric

**Contacts put on hold**  <a name="contacts-put-on-hold-historical"></a>
Count of contacts put on hold by an agent one or more times\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts queued**  <a name="contacts-queued-historical"></a>
Count of contacts placed in the queue\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts transferred in**  <a name="contacts-transferred-in-historical"></a>
Count of contacts transferred to the queue by an agent using the CCP\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts transferred in from queue**  <a name="contacts-transferred-in-from-queue-historical"></a>
Count of contacts transferred to the queue from another in a **Transfer to queue** contact flow\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts transferred out**  <a name="contacts-transferred-out-historical"></a>
Count of contacts transferred from the queue after being answered by an agent\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts transferred out external**  <a name="contacts-transferred-out-external-historical"></a>
Count of contacts that an agent transferred from the queue to an external source, such as a phone number other than the phone number for your contact center\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts transferred out from queue**  <a name="contacts-transferred-out-from-queue-historical"></a>
Count of contacts transferred from the queue to another queue in a **Transfer to queue** contact flow\.  
Type: Integer   
Category: CTR\-driven metric

**Contacts transferred out internal**  <a name="contacts-transferred-out-internal-historical"></a>
Count of contacts for the queue that an agent transferred to an internal source, such as a queue or another agent\. An internal source is any source that can be added as a Quick Connect\.  
Type: Integer   
Category: CTR\-driven metric

**Customer hold time**  <a name="customer-hold-time-historical"></a>
Total time that customers spent on hold after being connected to an agent\. This includes time spent on a hold when being transferred, but does not include time spent in a queue\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Error status time**  <a name="error-status-time-historical"></a>
For a specific agent, the total time contacts were in an error status\.  
Type: String \(*hh:mm:ss*\)  
Category: Agent activity\-driven metric

**Maximum queued time**  <a name="maimum-queued-time-historical"></a>
The longest time that a contact spent waiting in the queue\. This includes all contacts added to the queue, even if they were not connected with an agent, such as abandoned contacts\.  
Type: String \(*hh:mm:ss*\)  
Category: CTR\-driven metric

**Non\-Productive Time**  <a name="npt-historical"></a>
Total time that agents spent in a custom status \(any status other than **Available**, **Error**, or **Offline**\), including any time they spent handling contacts while in a custom status\. This metric can't be grouped or filtered by queue\.  
Type: String \(*hh:mm:ss*\)  
Category: Agent activity\-driven metric

**Occupancy**  <a name="occupancy-historical"></a>
Percentage of time that agents were active on contacts\. This percentage is calculated as follows:  
\(Agent Handle Time / \(Agent Handle Time \+ Agent Idle Time\)\) \* 100  
Type: String   
Min value: 0\.00%  
Max value: 100\.00%  
Category: Agent activity\-driven metric

**Online time**  <a name="online-time-historical"></a>
Total time that an agent spent in a status other than **Offline**\. This includes any time spent in a custom status\. This metric can't be grouped or filtered by queue\.  
Type: String \(*hh:mm:ss*\)  
Category: Agent activity\-driven metric

**Service level *X* seconds**  <a name="service-level-historical"></a>
Percentage of contacts removed from the queue between 0 and *X* seconds after being added to it\. A contact is removed from a queue when the following occurs: an agent answers the contact, the customer abandons the contact, or the customer requests a call back\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\. This percentage is calculated as follows:  
\(Contacts removed from queue in *X* seconds / Contacts queued\) \* 100  
Type: String   
Min value: 0\.00%  
Max value: 100\.00%  
Category: CTR\-driven metric