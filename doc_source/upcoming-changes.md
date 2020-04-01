# What's New in Metrics<a name="upcoming-changes"></a>

Thanks to your feedback, we've made changes to Amazon Connect metrics\. This topic gives you a overview of the improvements\. 

## Upcoming Changes for Omnichannel Support<a name="upcoming-changes-march-2020"></a>

### Group by Channel<a name="upcoming-changes-march-2020-channel"></a>

**To group queues or routing profiles by channel on real\-time metrics reports**

1. On the navigation menu, choose **Metrics and quality**, **Real\-time metrics**, and then select either **Queues** or **Routing profiles**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-queues-or-routing-profiles.png)

1. Choose **Settings**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-settings.png)

1. On the **Table Settings** page, choose the **Groupings** tab and then select **Queues grouped by channels**\. Or, if you're setting up a **Routing profiles** report, choose **Routing profiles grouped by channels**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-group-by-channel.png)

1. Choose **Apply**\.

1. The table will show a column for **Channel**\.

**To group by channel on historical metrics reports**

1. On the navigation menu, choose **Metrics and quality**, **Historical metrics**, and then choose a report\. 

1. Choose **Settings**\. 

1. On the **Table Settings** page, choose the **Groupings** tab\. Add **Channel**, and choose **Apply**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-grouping-channel.png)

1. The table will show a column for **Channel**, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-channel-label.png)

### Group by Queue in Historical Metrics Reports<a name="upcoming-changes-march-2020-queue-grouping"></a>

In the historical metrics report, when you group or filter metrics by **Queue**, the results for the following metrics aren't accurate: 
+ Agent idle time
+ Agent on contact time
+ Occupancy

Because of this, on the **Table Settings** page, **Metrics** tab, these metrics will be inactive, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-inactive-metrics.png)

In addition, in the historical metrics report, Amazon Connect will display a hyphen \(\-\) in place of results for these metrics, and the cells are inactive \(gray\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-null-metrics.png)

### Effect of Queue Grouping on Saved and Scheduled Reports<a name="upcoming-changes-march-2020-saved-scheduled-reports"></a>

If the **Queue** grouping or filter is used on the following reports, note these effects: 
+ **Saved reports**\. The columns for these metrics won't appear in the saved reports\.
+ **Scheduled reports**\. These reports will continue to run successfully, but no results will be returned for these metrics\. 

### Agent On Contact Time<a name="upcoming-changes-march-2020-agent-on-contact-time"></a>

On historical metrics reports when an agent handles multiple chats concurrently, **Agent on contact time** will show wall clock time: the amount of time spent chatting\. However, there isn't a metric that shows the time an agent spends chatting with each contact\.

In addition, no results will be returned when you use the **Queue** grouping or filter with **Agent On Contact Time**\.

### Agent Idle Time<a name="upcoming-changes-march-2020-agent-idle-time"></a>

The **Agent idle time** metric divides the idle time into each queue associated with the agent\. When contacts are grouped or filtered by **Queue**, however, Amazon Connect won't provide an accurate view into the how the agent is working\. Because of this, Amazon Connect won't show **Agent idle time** when you apply the **Queue** grouping or filter to your report\. 

### Occupancy<a name="upcoming-changes-march-2020-occupancy"></a>

With the addition of chat, the **Occupancy** metric is now defined as the percentage of time that an agent was active on contacts\. This percentage is calculated as follows:
+ \(Agent on contact \(wall clock time\) / \(Agent on contact \(wall clock time\) \+ Agent idle time\)\) 

Because **Agent idle time** is now inaccurate when contacts are grouped or filtered by **Queues**, the **Occupancy** metric is also inaccurate\. As a result, when contacts are grouped or filtered by Queues, **Occupancy** won't appear on the report\.

## November 2019: Name Changes for "Missed" and "Agent Status" and "On Call"<a name="upcoming-changes-names"></a>

The following real\-time metrics were renamed:


| Old Name | New Name | 
| --- | --- | 
|  Missed  | Agent non\-response  | 
|  Agent Status  | Agent Activity  | 
|  On Call  | On Contact  | 

For each metric, existing saved reports automatically start displaying the new name; you don't need to do anything for the new name to appear in your reports\. 

The column order for a saved report containing one of these metrics stays the same\. For example, if you previously saved a report where **Agent Status** was the third metric, now when you open that saved report, **Agent Activity** is the name for the third metric\.

For **Missed**, only the name of the metric changed; the underlying calculation stayed the same\. We've changing the name of this metric to **Agent non\-response** so it better reflects its definition: 
+ **Agent non\-response** increments whenever a contact is offered to an agent, and the agent doesn't respond to the contact for whatever reason\. 

  For example, the agent could have intentionally let the timer run out, or the agent could have forgotten to grant microphone access in the Contact Control Panel and never heard the ring\. In these situations, Amazon Connect doesn't drop the contact\. Instead, the routing engine will offer it to another available agent, while the customer continues to wait in queue\. This means a single contact could result in multiple **Agent non\-responses** before an agent responds and handles the contact\.

For **On Call**, the name change to **On Contact** applies to the Real\-time metrics UI only\. You can continue using `AGENTS_ON_CALL` with the ` GetCurrentMetricData` API to retrieve data for this metric\.

## Label Updates for "Agent Activity" and "Contact State"<a name="upcoming-changes-labels"></a>

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