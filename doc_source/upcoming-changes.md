# What's new in metrics<a name="upcoming-changes"></a>

Thanks to your feedback, we've made changes to Amazon Connect metrics\. This topic gives you an overview of the improvements\. 

## Upcoming change: 15 minutes interval for historical metrics reports<a name="metrics-changes-new-intervals-hmr"></a>

When customizing a historical metrics report, you will have the option to select a 15 minutes interval, in addition to the current option of a 30 minutes interval\. 

The 15 minutes interval works the same as the 30 minutes interval\. For example, you can query up to three days of data at a time, for the past 35 days\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-15-minute-interval.png)

## Upcoming changes: New metric groupings and categories<a name="metrics-changes-custom-service-levels"></a>

With the future release of [custom service level metrics](#custom-service-levels), we will also make the following changes:
+ On the **Table settings** pages, pre\-set and [custom service level metrics](#custom-service-levels) will be in a new group called **Contact Service Levels**\.
+ Historical metrics on the **Table settings** page will be grouped into categories\. Currently they are in a long, unordered list\.
+ The order of metric columns on historical metrics reports is changing to match the order of the metrics on the **Table settings** page\.

Following is more information about these changes\.

### Real\-time metrics: New Contact Service Level category<a name="custom-service-levels-rtm"></a>

A new category of metrics will be added to the **Table settings** page: **Contact Service Level**\.

The following image shows how this new category will appear on the **Table settings** page, in an expandable group\. Choose the arrow next to the group to view and select the metrics you want to add to your report\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-csl-groups.png)

Use the **Contact Service Level** category to choose pre\-set service level metrics, and to create custom service level metrics\.

The following image shows the user interface for creating custom service level metrics\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-create-csl.png)

### Historical metrics: New categories for metrics<a name="hmr-new-categories"></a>

To make it easier to find the historical metrics you want to add to a report, metrics on the **Table settings** page will be grouped into the following categories:
+ Agents
+ Contacts Abandoned
+ Contact Service Level: This group contains preset and custom service levels\.
+ Contacts Answered
+ Performance

Choose **Add Custom SL** to add custom service levels to your historical metrics report\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-csl-group.png)

### The order of the metric columns on the historical metrics reports is changing<a name="upcoming-changes-static-columns"></a>

The order of the metric columns on the historical metrics reports will match the updated grouping scheme and order of the metrics on the **Table settings** page\.

This change supports the addition of [custom service level metrics](#custom-service-levels)\. It will also allow us to make future improvements for where, for example, control of how a report looks resides on the **Real\-time metrics** page and the **Historical metrics** page, not the **Table settings** page\.

Note how metric columns will appear on reports in the upcoming release:
+ When you open the **Real\-time metrics** page, custom service levels will appear at the end of the **Performance** group\. 
+ Metrics on existing **Scheduled reports** \(the processed documents that arrive in your Amazon S3 buckets\) will not be re\-ordered automatically\. However, if you update an existing report, the metrics will be re\-ordered to match the order on the **Table settings** page\.
+ **Service level metrics**:
  + Real\-time metrics reports: Service level metrics will always be added to the end of the **Performance** group, in ascending order\. 
  + Historical metrics reports: When you add custom service level metrics, they will be added to the end of the report in the order they were created\.

## Upcoming change: Custom service level metrics<a name="custom-service-levels"></a>

Currently you can choose from pre\-set service levels in seconds\. In a future release, you will have the ability to add custom service level metrics\. You will also have the ability to choose from additional durations, such as minutes, hours, or days\.

The maximum duration for a custom service level is 7 days\. That's because in Amazon Connect you can't have a contact that goes longer than 7 days\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-custom-servicelevels.png)

## Upcoming change: Group by channel in a historical metrics report<a name="metrics-changes-group-by-channel-hmr"></a>

The following changes to the historical metrics report are upcoming in a future release\. 

**To group by channel on historical metrics reports**

1. On the navigation menu, choose **Metrics and quality**, **Historical metrics**, and then choose a report\. 

1. Choose **Settings**\. 

1. On the **Table Settings** page, choose the **Groupings** tab\. Add **Channel**, and choose **Apply**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-grouping-channel.png)

1. The table shows a column for **Channel**, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-channel-label.png)

## October 2020<a name="metrics-changes-october-2020"></a>

### New historical metrics for inbound and outbound contact time<a name="metrics-changes-inbound-outbound-contact-time-htm"></a>

Released the following real\-time metrics:
+  [Avg callback connecting time](real-time-metrics-definitions.md#rtm-avg-callback-connecting-time)
+ [Avg incoming connecting time](real-time-metrics-definitions.md#rtm-avg-incoming-connecting-time)
+  [Avg outbound connecting time](real-time-metrics-definitions.md#rtm-avg-outbound-connecting-time)

Released the following historical metrics:
+  [Agent API connecting time](historical-metrics-definitions.md#htm-agent-api-connecting-time)
+  [Agent callback connecting time](historical-metrics-definitions.md#htm-agent-callback-connecting-time)
+  [Agent incoming connecting time](historical-metrics-definitions.md#htm-agent-incoming-connecting-time)
+  [Agent outbound connecting time](historical-metrics-definitions.md#htm-agent-outbound-connecting-time)
+  [Average agent API connecting time](historical-metrics-definitions.md#htm-avg-agent-api-connecting-time)
+  [Average agent callback connecting time](historical-metrics-definitions.md#htm-avg-agent-callback-connecting-time)
+  [Average agent incoming connecting time](historical-metrics-definitions.md#htm-avg-agent-incoming-connecting-time)
+  [Average agent outbound connecting time](historical-metrics-definitions.md#htm-avg-agent-outbound-connecting-time)

### One\-click drill\-downs for Routing profiles and Queues tables<a name="metrics-changes-october-2020-one-click"></a>

In real\-time metrics reports, for **Routing profiles** and **Queues** tables, you can open pre\-filtered tables that display the associated queues, routing profiles, or agents\. These one\-click filters provide a way for you to drill into the performance data\.

For more information, see [Use one\-click drill\-downs for Routing profiles and Queues tables](one-click-drill-downs.md)

## June 2020: Changes for omnichannel support<a name="metrics-changes-june-2020"></a>

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
|  Agent is logged in but offline  |  Not shown  |  Not shown  |    | 
|  Agent switches to **Available** in the CCP  |  Available  |  Available  |    | 
|  Agent has an incoming call  |  CallIncoming  |  Incoming  |  ContactState = Incoming contact  | 
|  Agent has an incoming callback  |  CallbackIncoming  |  Incoming  |  ContactState = Inbound callback  | 
|  Agent accepted a callback, which is now making an outbound call to the customer  |  Calling  |  On Contact  |  ContactState = Outbound callback  | 
|  Agent makes outbound call \(regardless of what status the agent chose in their CCP\)  |  Calling  |  On Contact  |  ContactState = Outbound contact  | 
|  Agent missed a phone call due to timer expired  |  MissedCallAgent  |  Missed  |    | 
|  Agent is interacting with customer on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |    | 
|  Agent puts customer on hold while on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |    | 
|  After agent hangs up call  |  After call work  |  After contact work  |    | 
|  Agent is on Lunch \(a custom status\)  |  Lunch  |  Lunch  |    | 
|  Supervisor's activity state if they are monitoring some agent  |  Monitoring  |  Monitoring  |    | 
|  Agent's activity state if they are connected to customer while being monitored by a supervisor  |  On call  |  On Contact  |    | 

The following table shows the how the labels changed for **Contact State**\.


| Scenario | Label Name Before | Label Name After | 
| --- | --- | --- | 
|  Agent is logged in but offline  |    |    | 
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