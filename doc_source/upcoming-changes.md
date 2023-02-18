# What's new in metrics<a name="upcoming-changes"></a>

Thanks to your feedback, we've made changes to Amazon Connect metrics\. This topic gives you an overview of the improvements\. 

## November 2022<a name="new-queue-dashboard-hmr-nov2022"></a>

The following updates were released in November 2022\.

**Manage saved reports \(admin\)**

You can view and delete all saved reports in your instance, including reports that were not created by you or that are not currently published\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-queue-dashboard-saved-reports.png)

## September 2022<a name="new-queue-dashboard-hmr-sept2022"></a>

The following updates were released in September 2022\.

**Queue Dashboard**

You can now visualize historical queue data via time series graphs to help identify patterns, trends and outliers specifically for Service Level, Contacts Queued, and Average Handle Time\. To visualize your queue data, select **View queue graphs** from the queue dropdown\. Once selected, you will be directed to the queue visualization dashboard where you can configure *Time* range \(up to 24 hours\) and *Channel*\. You also have the ability to customize the service level thresholds\.

**Navigate to Queue dashboard**

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-queue-dashboard-ui.png)

**Queue dashboard experience**

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-queue-dashboard-exp.png)

## June 2022<a name="new-15-minute-historical-schedules-hmr-june2022"></a>

The following updates were released in June 2022\.

**15 minute scheduled reports**

You can now schedule historical metrics to refresh every 15 minutes\. To select 15\-minute schedules, select generate this report **Hourly** every \.25 hours \(this is the top most option in the second dropdown\), for the previous \.25 hours\. The following image shows the values that you need to select\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-15-minute-scheduled-reports.png)

## <a name="new-real-time-metrics-agent-table-by-agent-june2022"></a>

**Filter Real\-Time Metrics Agent Table by Agent**

You can now filter the agent table on the Real\-Time Metrics page by agent\. This filter functions the same as the existing queues, routing profiles, and agent hierarchy filters\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-rtm-agent-filtering.png)

## New contact transferred related metrics<a name="contact-transferred-whats-new"></a>

We are upgrading the existing [Contacts transferred in](historical-metrics-definitions.md#contacts-transferred-in-historical) and [Contacts transferred out](historical-metrics-definitions.md#contacts-transferred-out-historical) historical metrics to have consistent definitions\. We are adding [Contacts transferred in by agent](historical-metrics-definitions.md#contacts-transferred-in-by-agent-historical) and [Contacts transferred out by agent](historical-metrics-definitions.md#contacts-transferred-out-by-agent-historical) for more granular contact transferred related metrics\. 

## Changes to real\-time metrics agent tables<a name="agent-tables-rtm-page"></a>

We are rolling out a new service to maintain the high availability from metrics that you expect from Amazon Connect\. Due to this change, the agent tables are sorted by [agent status](metrics-agent-status.md) instead of by agent login\.

Additionally, the queues and routing profiles table are sorted by agents online instead of by queue or routing profile name\.

## Faster reload times for the Real\-time metrics page<a name="upgrading-rtm-page"></a>

We are upgrading the performance of the **Real\-time metrics** page so reload times are faster\. The page will have the same functionality and user experience as the existing **Real\-time metrics** page\.

## April 2021<a name="metrics-changes-chat-metrics-april2021"></a>

The following updates were released in April 2021\.
+ Amazon Connect incorrectly reported that chat contacts that were created from disconnect flows were created from transfer flows\.
+ With these fixes, Amazon Connect correctly reflects in the contact records and agent event stream that these chat contacts were created from disconnect flows\. 

There is no impact to voice or task contacts\. 

Chat contacts created through disconnect flows no longer increment the following metrics: 
+ [Contact flow time](historical-metrics-definitions.md#contact-flow-time-historical) 
+ [Contacts incoming](historical-metrics-definitions.md#contacts-incoming-historical)
+ [Contacts handled incoming](historical-metrics-definitions.md#contacts-handled-incoming-historical)
+ [Contacts transferred in](historical-metrics-definitions.md#contacts-transferred-in-historical)

In addition, note the following fixes for contact records and the agent event stream for chat contacts:
+ Contact records: There was an issue in the **Attributes** section of a chat contact record where the initiation method is **API** for both disconnect and transfer contacts\. With this fix, the initiation method correctly reflect **Disconnect** and **Transfer**, respectively\. 
+ Agent event stream: Chat contacts created from disconnect flows now have **Disconnect** as the initiation method\. 

## March 2021<a name="metrics-changes-new-intervals-hmr-march2021"></a>

The following updates were released in March 2021\.

When customizing a historical metrics report, you have the option to select a 15 minutes interval, in addition to the current option of a 30 minutes interval\. 

The 15 minutes interval works the same as the 30 minutes interval\. For example, you can query up to three days of data at a time, for the past 35 days\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-15-minute-interval.png)

## February 2021<a name="metrics-changes-february-2021"></a>

The following updates were released in February 2021\. 

### New metric groupings and categories<a name="metrics-changes-custom-service-levels"></a>

With the release of [custom service level metrics](#custom-service-levels), we also made the following changes:
+ On the **Table settings** pages, pre\-set and [custom service level metrics](#custom-service-levels) are in a new group called **Contact Service Levels**\.
+ Historical metrics on the **Table settings** page are grouped into categories\. 
+ The order of metric columns on historical metrics reports changed to match the order of the metrics on the **Table settings** page\.

Following is more information about these changes\.

#### Real\-time metrics: New Contact Service Level category<a name="custom-service-levels-rtm"></a>

A new category of metrics appears on the **Table settings** page: **Contact Service Level**\.

The following image shows this new category on the **Table settings** page, in an expandable group\. Choose the arrow next to the group to view and select the metrics you want to add to your report\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-csl-groups.png)

Use the **Contact Service Level** category to choose pre\-set service level metrics, and to create custom service level metrics\.

The following image shows the user interface for creating custom service level metrics\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-create-csl.png)

#### Historical metrics: New categories for metrics<a name="hmr-new-categories"></a>

To make it easier to find the historical metrics you want to add to a report, metrics on the **Table settings** page are grouped into the following categories:
+ Agents
+ Contacts Abandoned
+ Contact Service Level: This group contains preset and custom service levels\.
+ Contacts Answered
+ Performance

Choose **Add Custom SL** to add custom service levels to your historical metrics report\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-csl-group.png)

#### The order of the metric columns on the historical metrics reports has changed<a name="upcoming-changes-static-columns"></a>

The order of the metric columns on the historical metrics reports matches the updated grouping scheme and order of the metrics on the **Table settings** page\.

This change supports the addition of [custom service level metrics](#custom-service-levels)\. It also allows us to make future improvements for where, for example, control of how a report looks resides on the **Real\-time metrics** page and the **Historical metrics** page, not the **Table settings** page\.

Note how metric columns now appear on reports:
+ When you open the **Real\-time metrics** page, custom service levels appear at the end of the **Performance** group\. 
+ Metrics on existing **Scheduled reports** \(the processed documents that arrive in your Amazon S3 buckets\) are not re\-ordered automatically\. However, if you update an existing report, the metrics are re\-ordered to match the order on the **Table settings** page\.
+ **Service level metrics**:
  + Real\-time metrics reports: Service level metrics are always added to the end of the **Performance** group, in ascending order\. 
  + Historical metrics reports: When you add custom service level metrics, they are added to the end of the report in the order they were created\.

### Custom service level metrics<a name="custom-service-levels"></a>

You have the ability to add custom service level metrics\. You can also choose from additional durations, such as minutes, hours, or days\.

The maximum duration for a custom service level is 7 days\. That's because in Amazon Connect you can't have a contact that goes longer than 7 days\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-custom-servicelevels.png)

### Group by channel in a historical metrics report<a name="metrics-changes-group-by-channel-hmr"></a>

**To group by channel on historical metrics reports**

1. On the navigation menu, choose **Analytics and optimization**, **Historical metrics**, and then choose a report\. 

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

1. On the navigation menu, choose **Analytics and optimization**, **Real\-time metrics**, and then select either **Queues** or **Routing profiles**\.   
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