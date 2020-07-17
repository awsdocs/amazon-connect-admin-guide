# What's new in metrics<a name="upcoming-changes"></a>

Thanks to your feedback, we've made changes to Amazon Connect metrics\. This topic gives you a overview of the improvements\. 

## Upcoming changes: New real\-time metrics for inbound and outbound contact time<a name="metrics-changes-inbound-outbound-contact-time-rtm"></a>

The following new real\-time metrics are upcoming in a future release\. 

### Avg incoming connecting time<a name="rtm-avg-incoming-connecting-time"></a>

The average time between when contacts are initiated Amazon Connect reserving the agent for the contact, and the agent is connected\. 

In the agent event stream, this time is calculated by averaging the duration between the contact state of STATE\_CHANGE event changes from CONNECTING to CONNECTED/MISSED/ERROR\. 

The following image shows the three parts that go into calculating **Avg incoming connecting time**\. It also shows what is in the agent event stream\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-agent-inbound-connection-time.png)

### Avg outbound connecting time<a name="rtm-avg-outbound-connecting-time"></a>

The average time between when outbound contacts are initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

The following image shows the four parts that go into calculating **Avg outbound connecting time**\. It also shows what is in the agent event stream\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-agent-outbound-connection-time.png)

### Avg callback connecting time<a name="rtm-avg-callback-connecting-time"></a>

Then average time between when callback contacts are initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

The following image shows the five parts that go into calculating **Avg callback connecting time**\. It also shows what is in the agent event stream\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-agent-callback-connection-time.png)

## Upcoming changes: New historical metrics for inbound and outbound contact time<a name="metrics-changes-inbound-outbound-contact-time-htm"></a>

The following new historical metrics are upcoming in a future release\. 

### Agent incoming connecting time<a name="htm-agent-incoming-connecting-time"></a>

The total time between when a contact is initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\.

In the agent event stream, this is the duration between the contact state of STATE\_CHANGE event changes from CONNECTING to CONNECTED/MISSED/ERROR\. 

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Agent outbound connecting time<a name="htm-agent-outbound-connecting-time"></a>

The total time between when an outbound contact is initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\.

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Agent callback connecting time<a name="htm-agent-callback-connecting-time"></a>

The total time between when a callback contact is initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\.

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Agent API connecting time<a name="htm-agent-api-connecting-time"></a>

The total time between when a contact is initiated using an Amazon Connect API, and the agent is connected\.

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Average agent incoming connecting time<a name="htm-avg-agent-incoming-connecting-time"></a>

The average time between when contact is initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Average agent outbound connecting time<a name="htm-avg-agent-outbound-connecting-time"></a>

The average time between when an outbound contact is initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Average agent callback connecting time<a name="htm-avg-agent-callback-connecting-time"></a>

The average time between when a callback contact is initiated by Amazon Connect reserving the agent for the contact, and the agent is connected\. 

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

### Average agent API connecting time<a name="htm-avg-agent-api-connecting-time"></a>

The average time between when a contact is initiated using an Amazon Connect API, and the agent is connected\. 

Type: String \(hh:mm:ss\)

Category: Agent activity\-driven metric

## June 2020: Changes for omnichannel spport<a name="metrics-changes-june-2020"></a>

### Group by channel<a name="metrics-changes-june-2020-channel"></a>

**To group queues or routing profiles by channel on real\-time metrics reports**

1. On the navigation menu, choose **Metrics and quality**, **Real\-time metrics**, and then select either **Queues** or **Routing profiles**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-queues-or-routing-profiles.png)

1. Choose **Settings**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-settings.png)

1. On the **Table Settings** page, choose the **Groupings** tab and then select **Queues grouped by channels**\. Or, if you're setting up a **Routing profiles** report, choose **Routing profiles grouped by channels**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-group-by-channel.png)

1. Choose **Apply**\.

1. The table shows a column for **Channel**\.

**To group by channel on historical metrics reports**

1. On the navigation menu, choose **Metrics and quality**, **Historical metrics**, and then choose a report\. 

1. Choose **Settings**\. 

1. On the **Table Settings** page, choose the **Groupings** tab\. Add **Channel**, and choose **Apply**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-grouping-channel.png)

1. The table shows a column for **Channel**, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-channel-label.png)

### Group by queue in historical metrics reports<a name="metrics-changes-june-2020-queue-grouping"></a>

In the historical metrics report, when you group or filter metrics by **Queue**, the results for the following metrics aren't accurate: 
+ Agent idle time \(not supported in queue grouping as of June, 2020\)
+ Agent on contact time \(not supported in queue grouping as of June, 2020\)
+ Occupancy \(not supported in queue grouping as of June, 2020\)

Because of this, on the **Table Settings** page, **Metrics** tab, these metrics are inactive, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-inactive-metrics.png)

In addition, in the historical metrics report, Amazon Connect displays a hyphen \(\-\) in place of results for these metrics, and the cells are inactive \(gray\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-null-metrics.png)

### Effect of queue grouping on saved and scheduled reports<a name="metrics-changes-june-2020-saved-scheduled-reports"></a>

If the **Queue** grouping or filter is used on the following reports, note these effects: 
+ **Saved reports**\. The columns for these metrics don't appear in the saved reports when *grouped* by Queue\. When the saved report is *filtered* by Queue, however, it shows "\-"\.
+ **Scheduled reports**\. These reports continue to run successfully, but no results are returned for these metrics\. 

### Agent on contact time \(not supported in queue grouping as of June, 2020\)<a name="metrics-changes-june-2020-agent-on-contact-time"></a>

On historical metrics reports when an agent handles multiple chats concurrently, **Agent on contact time** shows wall clock time: the amount of time spent chatting\. However, there isn't a metric that shows the time an agent spends chatting with each contact\.

In addition, no results are returned when you use the **Queue** grouping or filter with **Agent on contact time**\.

### Agent idle time \(not supported in queue grouping as of June, 2020<a name="metrics-changes-june-2020-agent-idle-time"></a>

The **Agent idle time** metric divides the idle time into each queue associated with the agent\. When contacts are grouped or filtered by **Queue**, however, Amazon Connect doesn't provide an accurate view into the how the agent is working\. Because of this, Amazon Connect doesn't show **Agent idle time** when you apply the **Queue** grouping or filter to your report\. 

### Occupancy \(not supported in queue grouping as of June, 2020\)<a name="metrics-changes-june-2020-occupancy"></a>

With the addition of chat, the **Occupancy** metric is now defined as the percentage of time that an agent was active on contacts\. This percentage is calculated as follows:
+ \(Agent on contact \(wall clock time\) / \(Agent on contact \(wall clock time\) \+ Agent idle time\)\) 

Because **Agent idle time** is now inaccurate when contacts are grouped or filtered by **Queues**, the **Occupancy** metric is also inaccurate\. As a result, when contacts are grouped or filtered by Queues, **Occupancy** doesn't appear on the report\.

Occupancy no longer appears on the **Dashboard** page\.

## November 2019<a name="metrics-changes-november-2019"></a>

### Name changes for "Missed" and "Agent status" and "On call"<a name="metrics-changes-november-2019-names"></a>

The following real\-time metrics were renamed:


| Old name | New name | 
| --- | --- | 
|  Missed  | Agent non\-response  | 
|  Agent status  | Agent activity  | 
|  On call  | On contact  | 

For each metric, existing saved reports automatically start displaying the new name; you don't need to do anything for the new name to appear in your reports\. 

The column order for a saved report containing one of these metrics stays the same\. For example, if you previously saved a report where **Agent status** was the third metric, now when you open that saved report, **Agent activity** is the name for the third metric\.

For **Missed**, only the name of the metric changed; the underlying calculation stayed the same\. We've changing the name of this metric to **Agent non\-response** so it better reflects its definition: 
+ **Agent non\-response** increments whenever a contact is offered to an agent, and the agent doesn't respond to the contact for whatever reason\. 

  For example, the agent could have intentionally let the timer run out, or the agent could have forgotten to grant microphone access in the Contact Control Panel and never heard the ring\. In these situations, Amazon Connect doesn't drop the contact\. Instead, the routing engine will offer it to another available agent, while the customer continues to wait in queue\. This means a single contact could result in multiple **Agent non\-responses** before an agent responds and handles the contact\.

For **On call**, the name change to **On Contact** applies to the Real\-time metrics UI only\. You can continue using `AGENTS_ON_CALL` with the `GetCurrentMetricData` API to retrieve data for this metric\.

### Label updates for "Agent activity" and "Contact state"<a name="metrics-changes-november-2019-labels"></a>

Labels are the values returned in a report\. For example, in the following image **Available** and **Basic Routing Profile** are labels\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/labels.png)

For **Agent Activity** and **Contact State**, we renamed some of the labels that describe what the agent's current activity is and what's happening with the contact they are currently working on\. This way, the labels in the Real\-Time Metrics report are more consistent with the labels the agent sees in the Contact Control Panel\. They also align with the data returned about these different states in other parts of Amazon Connect\.

When the name of **Agent Status** changed to **Agent Activity**, the following labels changed, too:


| Scenario | Before: Agent Status Labels | After: Agent Activity Labels | Notes | 
| --- | --- | --- | --- | 
|  Agent is logged in but offline  |  Not shown  |  Not shown  |   | 
|  Agent switches to **Available** in the CCP  |  Available  |  Available  |   | 
|  Agent has an incoming call  |  CallIncoming  |  Incoming  |  ContactState = Incoming contact  | 
|  Agent has an incoming callback  |  CallbackIncoming  |  Incoming  |  ContactState = Inbound callback  | 
|  Agent accepted a callback, which is now making an outbound call to the customer  |  Calling  |  On Contact  |  ContactState = Outbound callback  | 
|  Agent makes outbound call \(regardless of what status the agent chose in their CCP\)  |  Calling  |  On Contact  |  ContactState = Outbound contact  | 
|  Agent missed a phone call due to timer expired  |  MissedCallAgent  |  Missed  |   | 
|  Agent is interacting with customer on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |   | 
|  Agent puts customer on hold while on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |   | 
|  After agent hangs up call  |  After call work  |  After contact work  |   | 
|  Agent is on Lunch \(a custom status\)  |  Lunch  |  Lunch  |   | 
|  Supervisor's activity state if they are monitoring some agent  |  Monitoring  |  Monitoring  |   | 
|  Agent's activity state if they are connected to customer while being monitored by a supervisor  |  On call  |  On Contact  |   | 

The following table shows the how the labels changed for **Contact State**\.


| Scenario | Label Name Before | Label Name After | 
| --- | --- | --- | 
|  Agent is logged in but offline  |   |   | 
|  Agent switches to **Available** in the CCP  | \-  | \-  | 
|  Agent has an incoming call  |  \-  |  Incoming contact  | 
|  Agent has an incoming callback  |  \-  |  Inbound callback  | 
|  Agent accepted a callback, which is now making an outbound call to the customer  |  Initial  |  Outbound callback  | 
|  Agent makes outbound call \(regardless of what status the agent chose in their CCP\)  |  Initial  |  Outbound contact  | 
|  Agent missed a phone call due to timer expired  |  Missed call  |  Missed contact  | 
|  Agent is interacting with customer on phone call \(regardless of what status the agent chose in their CCP\)  |  Busy  |  Connected  | 
|  Agent puts customer on hold while on phone call \(regardless of what status the agent chose in their CCP\)  |  OnHold  |  On hold  | 
|  After agent hangs up call  |  After call work  |  After contact work  | 
|  Agent is on Lunch \(a custom status\)  |  \-  |  \-  | 
|  Supervisor's contact state if they are monitoring an agent  |  Monitoring  |  Monitoring  | 