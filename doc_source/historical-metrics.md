# Historical Metrics Reports<a name="historical-metrics"></a>

Historical metrics reports include data about past, completed activity and performance in your contact center\. You can customize the report settings to get the view of the data that is most meaningful for your organization\. You can change the time frame for the report, which metrics are included in the report, and how data is grouped in the report\. After you have customized a report, you can save it for future reference\. You can generate a report using a recurring schedule that you define\.

**Topics**
+ [Grouping Options](#historical-metrics-groupings)
+ [Filters](#historical-metrics-filters)
+ [Create a Historical Metrics Report](#create-historical-metrics-report)
+ [Schedule a Historical Metrics Report](#schedule-historical-metrics-report)
+ [Update a Historical Metrics Report](#update-historical-metrics-report)
+ [Download a Historical Metrics Report](#download-historical-metrics-report)
+ [Historical Metrics Definitions](#historical-metrics-definitions)

## Grouping Options<a name="historical-metrics-groupings"></a>

You can group the metrics included in your reports in different ways to provide greater insight into how your contact center is performing\.

You can group reports by queue, agent, agent hierarchy, routing profile, or phone number\. The metric calculations, and therefore metrics values displayed in the report, are different when reports are grouped differently\. For example, if you group a report by queue, the value of a metric includes all contacts associated with the queue\. If you group a report by agent, the values for the metrics associated with queues might not provide much insight\.

When you create a report, the values for calculated metrics are displayed as rows in the report\. The rows in the report are grouped by the grouping options you select\. Grouping the data enables you to generate global data for your contact center, or more specific data for queues, agents, routing profiles, or agent hierarchy defined in your contact center\.

For example, consider the **Contacts handled** metric\. This metric is a count of the contacts handled during the time range defined for the report\. Here are the results based on the grouping:
+ **Queue** \- The metric is the total number of contacts handled during the time range from that queue by all agents in your contact center\.
+ **Agent** \- The metric is the total number of contacts handled by that agent during the time range across all queues and routing profiles\.
+ **Routing Profile** \- The metric is the total number of contacts handled during the time range by agents assigned that routing profile\.
+ **Queue**, then **Agent**, then **Routing Profile** \- The metric is the total number of contacts that agent assigned that routing profile handled from that queue\.

Agent activity can be included in one routing profile at a time, but agents can switch between routing profiles over the reporting time interval\. If agents are assigned multiple routing profiles and handle contacts from multiple queues, there are multiple rows in the report for each routing profile assigned to the agent and the queue that the agent handled contacts from\.

## Filters<a name="historical-metrics-filters"></a>

When you customize a report, you can add filters to control which data is included in the report\. You can filter on the following:
+ **Queue**—Includes data only for the specified queues\. If you do not specify any queues, all queues are included\.
+ **Routing profile**—Includes data only for the agents assigned to the specified routing profiles\. If you do not specify any routing profiles, data for all agents for all routing profiles is included\.
+ **Agent hierarchy**—Includes data only for the contacts handled by agents in the specified hierarchies\. If you do not specify a hierarchy, data for all contacts handled by agents in all hierarchies is included\. When only one hierarchy is specified, you can specify a more granular filter within the hierarchy\.
+ **Phone number**—Includes data only for the contacts associated with the specified phone numbers\. If you do not specify a phone number, data for all contacts associated with all phone numbers is included\.

## Create a Historical Metrics Report<a name="create-historical-metrics-report"></a>

You can create historical metrics reports to view data for past activity in your contact center\.

**Requirement**
+ You must have permission to access metric data\. The following security profiles include this permission: **CallCenterManager** and **QualityAnalyst**\. For more information, see [Amazon Connect Security Profiles](connect-security-profiles.md)\.

**Limits**
+ You can get data only for active queues\. A queue is inactive if there are no contacts in the queue and no agents available\.
+ The user interface shows up to 100 queues\. If you have more than 100 active queues, you can add a filter to scope the report to the queues of interest\.
+ A report can contain up to 80K cells \(*columns* \* *rows*\)\.

**To create a historical metrics report**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Metrics and quality**, **Historical metrics**\.

1. Choose one of the following report types, which group and order the data in different ways, and include different metrics:
   + **Queues**
     + **Contact metrics**
     + **Agent metrics**
   + **Agents**
     + **Agent performance**
   + **Phone numbers**
     + **Contact metrics**

1. To customize your report, choose the gear icon\.

1. On the **Interval & Time range** tab, do the following:

   1. For **Interval**, choose **30 minutes** to get a row for each 30\-minute period in the time range, **Daily** to get a row for each day in the time range, or **Total** to get all data for the time range in a single row\.

   1. For **Time Zone**, select a time zone, which determines the hour at which a day starts\. For example, to align the report with your calendar days, select the time zone for your location\.

      You should use the same time zone for reports over time to get accurate and consistent metrics data for your contact center\. Using different time zones for different reports may result in different data for the same time range selection\.

   1. The possible values for **Time range** depend on the value that you select for **Interval**\. Alternatively, you can specify a custom time range\.

      For **Last *x* days** and **Month to date**, the current day is not included in the report\. **Yesterday** specifies the previous calendar day while **Last 24 hours** specifies the 24 hours prior to the current time\.

1. \(Optional\) On the **Groupings** tab, chose up to five groupings\. If you choose one grouping option, the data is grouped by that option\. If you choose multiple grouping options, the data is group by the first grouping option and then by the subsequent grouping options\. For more information, see [Grouping Options](#historical-metrics-groupings)\.

1. \(Optional\) On the **Filters** tab, specify filters to scope the data to be included in the report\. The available filters depend on the groupings that you select\. For more information, see [Filters](#historical-metrics-filters)\.

1. On the **Metrics** tab, choose the metrics and fields to include in the report\. An exclamation point \(\!\) is displayed next to any metrics that are not available based on the groupings that you selected\. For more information, see [Historical Metrics Definitions](#historical-metrics-definitions)\.

1. When you are finished customizing your report, choose **Apply**\.

1. \(Optional\) To save your report for future use, choose **Save**, provide a name for the report, and then choose **Save**\.

## Schedule a Historical Metrics Report<a name="schedule-historical-metrics-report"></a>

Scheduling a report makes the report accessible by any other users for your contact center that have permissions to view saved reports\. Any user with permission to edit saved reports can also modify your scheduled reports\. Scheduled reports are saved as CSV files in the Amazon S3 bucket specified for reports for your contact center\. When you set up the scheduled report, you can add a prefix to the location in Amazon S3 for the report files\.

For scheduled reports, there is a delay of 15 minutes after the scheduled report time before the report is generated\. This is to ensure that the report includes the data for all of the activity that occurred during the time range specified for the report\. Data from your contact center is not immediately processed and available to include in reports, so some data from the time range might not be captured in a report if the report is generated at the second the time range ends\. For example, if you create a scheduled report for time frame of 8:00 AM to 5:00 PM, and there is activity in your contact center between 4:46:00 PM and 4:59:59 PM, the data about that activity may not be aggregated prior 5:00 PM when the report is scheduled to generate\. Instead, the report is generated after 5:15 PM, by which time the data for the last 15 minutes of the time range is included in the report\.

**To schedule a historical metrics report**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Create a new report and save it, or open a saved report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Schedule**\.

1. On the **Recurrence** tab, specify the pattern for the recurrence \(for example, weekly on Saturdays\) and the range \(for example, from midnight for the previous 5 days\)\.

1. \(Optional\) On the **Delivery Options** tab, specify a prefix for the location in Amazon S3 for the report files\.

## Update a Historical Metrics Report<a name="update-historical-metrics-report"></a>

After you save a report, you can update it at any time\.

**To update a historical metrics report**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Metrics and quality**, **Saved reports**\.

1. From the **Historical metrics** tab, choose the name of the report\. Choose the gear icon, update the report settings as needed, and choose **Apply**\.

1. To update the current report, choose **Save**\. To save your changes to a new report, choose **Save as**\.

## Download a Historical Metrics Report<a name="download-historical-metrics-report"></a>

You can download the data included in a report as a comma\-separated value \(CSV\) file, so that you can use it with other applications\. If there is no data for one of the selected metrics, the field in the downloaded CSV file contains a dash\.

When the report is exported to your Amazon S3 bucket, the file name for the exported file includes the date and UTC time at which the report was created\. The **Last modified date** for the file is displayed using the time zone for the Amazon S3 bucket, and may not match the creation time for the report, which is in UTC\.

**To download a historical metrics report as a CSV file**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Create a new report or open a saved report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Download CSV**\.

1. When prompted, confirm whether to open or save the file\.

## Historical Metrics Definitions<a name="historical-metrics-definitions"></a>

The following metrics are available to include in historical metrics reports in Amazon Connect\.

**After contact work time**  <a name="acw-historical"></a>
Total time that an agent spent in the After Contact Work \(ACW\) status after handling a contact\. Agents enter the ACW status after a contact ends and leave it when they select a different agent status\.

**Agent answer rate**  <a name="agent-answer-rate-historical"></a>
Percentage of contacts routed to an agent that were answered\.

**Agent first name**  <a name="agent-first-name-historical"></a>
The first name of the agent, as entered in their Amazon Connect user account\. This metric is available only when grouping by agent\.

**Agent idle time**  <a name="agent-idle-time-historical"></a>
Total time that an agent spent in a productive status without handling contacts\. The productive statuses include **Available** and **Error**\.

**Agent interaction and hold time**  <a name="agent-interaction-hold-time-historical"></a>
Sum of the **Agent interaction time** and **Customer hold time** metrics\.

**Agent interaction time**  <a name="agent-interaction-time-historical"></a>
Total time that agents spent interacting with customers on a contact\. This does not include hold time or after contact work\.

**Agent last name**  <a name="agent-last-name-historical"></a>
The last name of the agent, as entered in their Amazon Connect user account\. This metric is available only when grouping by agent\.

**Agent name**  <a name="agent-name-historical"></a>
The name of the agent, displayed as follows: **Agent last name**, **Agent first name**\. This metric is available only when grouping by agent\.

**Agent non\-response**  <a name="agent-non-response"></a>
Count of contacts routed to an agent but not answered by the agent, including contacts abandoned by the customer\. A contact can be counted as missed multiple times, once for each time it is routed to an agent but not answered\.  
This metric appears as **Contacts missed** in scheduled reports and exported CSV files\.

**Agent on contact time**  <a name="agent-on-contact-time-historical"></a>
Total time that an agent spent on a contact, including hold time and after contact work\. This does not include time spent on a contact while in a custom status\.

**API contacts**  <a name="api-contacts-historical"></a>
Count of contacts that were initiated using an Amazon Connect API operation, such as `StartOutboundVoiceContact`\. This includes contacts that were not handled by an agent\.

**API contacts handled**  <a name="api-contacts-handled-historical"></a>
Count of contacts that were initiated using an Amazon Connect API operation, such as `StartOutboundVoiceContact`, and handled by an agent\.

**Average after contact work time**  <a name="average-acw-time-historical"></a>
Average time that an agent spent in the After Contact Work \(ACW\) status\. This is calculated by averaging `AfterContactWorkDuration` \(from the CTR\) for all contacts included in the report, based on the selected filters\.

**Average agent interaction and customer hold time**  <a name="average-agent-interaction-customer-hold-time-historical"></a>
Average of the sum of the agent interaction and customer hold time\. This is calculated by averaging the sum of the following values from the CTR: `AgentInteractionDuration` and `CustomerHoldDuration`\.

**Average agent interaction time**  <a name="average-agent-interaction-time-historical"></a>
Average time that agents interacted with customers during contacts\.

**Average customer hold time**  <a name="average-customer-hold-time-historical"></a>
Average time that customers spent on hold while connected to an agent\. This is calculated by averaging `CustomerHoldDuration` \(from the CTR\)\.

**Average handle time**  <a name="average-handle-time-historical"></a>
Average time that agents spent on contacts, including hold time and after contact work\.

**Average outbound after contact work time**  <a name="average-outbound-acw-time-historical"></a>
Average time that agents spent in the After Contact Work \(ACW\) status after an outbound contact\.

**Average outbound agent interaction time**  <a name="average-outbound-agent-interaction-time-historical"></a>
Average time that agents spent interacting with a customer during an outbound contact\.

**Average queue abandon time**  <a name="average-queue-abandon-time-historical"></a>
Average time that contacts waited in the queue before being abandoned\. This is calculated by averaging the difference between `EnqueueTimestamp` and `DequeueTimestamp` \(from the CTR\) for abandoned contacts\. An contact is considered abandoned if it was removed from a queue but not answered by an agent or queued for callback\.

**Average queue answer time**  <a name="average-queue-answer-time-historical"></a>
Average time that contacts waited in the queue before being answered by an agent\. This is the average of `Duration` \(from the CTR\)\.

**Callback contacts**  <a name="callback-contacts-historical"></a>
Count of contacts that were initiated from a queued callback\.

**Callback contacts handled**  <a name="callback-contacts-handled-historical"></a>
Count of contacts that were initiated from a queued callback and handled by an agent\.

**Contact flow time**  <a name="contact-flow-time-historical"></a>
Total time a contact spent in a contact flow\.  
Outbound contacts do not start in a contact flow, so outbound contacts are not included\.

**Contact handle time**  <a name="contact-handle-time-historical"></a>
Total time that an agent spent on contacts, including hold time and **After contact work time**\. This includes any time spent on contacts while in a custom status\. Note that the time spent in a custom status is not available in the CTR or as a separate metric\.

**Contacts abandoned**  <a name="contacts-abandoned-historical"></a> Contacts abandoned is a metric that works for queue or phone number groupings
Count of contacts disconnected by the customer while in the queue\. This metric can only be grouped by Queue or Phone Number groupings. Contacts queued for callback are not counted as abandoned\.

**Contacts abandoned in *X* seconds**  <a name="contacts-abandoned-x-historical"></a>
Count of contacts disconnected by the customer while in the queue for 0 to *X* seconds\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\.

**Contacts agent hung up first**  <a name="contacts-agent-hung-up-first-historical"></a>
Count of contacts disconnected where the agent disconnected before the customer\.

**Contacts answered in *X* seconds**  <a name="contacts-answered-x-historical"></a>
Count of contacts that were answered by an agent between 0 and *X* seconds of being placed in the queue, based on the value of `EnqueueTimestamp`\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\.

**Contacts consulted**  <a name="contacts-consulted-historical"></a>
Count of contacts handled by an agent who consulted with another agent in Amazon Connect\. The agent interacts with the other agent, but the customer is not transferred to the other agent\.

**Contacts handled**  <a name="contacts-handled-historical"></a>
Count of contacts handled by an agent, including both incoming and outgoing contacts\.

**Contacts handled incoming**  <a name="contacts-handled-incoming-historical"></a>
Count of incoming contacts that were handled by an agent, including inbound contacts, transferred contacts, and scheduled callbacks\.

**Contacts handled outbound**  <a name="contacts-handled-outbound-historical"></a>
Count of outbound contacts that were handled by an agent\. This includes contacts that were initiated by an agent using the CCP\.

**Contacts hold agent disconnect**  <a name="contacts-hold-agent-disconnect-historical"></a>
Count of contacts that were disconnected by the agent while the customer was on hold\.

**Contacts hold customer disconnect**  <a name="contacts-hold-customer-disconnect-historical"></a>
Count of contacts that were disconnected by the customer while the customer was on hold\.

**Contacts hold disconnect**  <a name="contacts-hold-disconnect-historical"></a>
Count of contacts disconnected while the customer was on hold\. This includes both contacts disconnected by the agent and contacts disconnected by the customer\.

**Contacts incoming**  <a name="contacts-incoming-historical"></a>
Count of incoming contacts, including inbound contacts and transferred contacts\.

**Contacts missed**  <a name="contacts-missed-historical"></a>
Count of contacts routed to an agent but not answered by the agent, including contacts abandoned by the customer\. A contact can be counted as missed multiple times, once for each time it is routed to an agent but not answered\.  
This metric appears as **Agent non\-response** on the **Historical metrics** page in the user interface\.

**Contacts put on hold**  <a name="contacts-put-on-hold-historical"></a>
Count of contacts put on hold by an agent one or more times\.

**Contacts queued**  <a name="contacts-queued-historical"></a>
Count of contacts placed in the queue\.

**Contacts transferred in**  <a name="contacts-transferred-in-historical"></a>
Count of contacts transferred to the queue by an agent using the CCP\.

**Contacts transferred in from queue**  <a name="contacts-transferred-in-from-queue-historical"></a>
Count of contacts transferred to the queue from another in a **Transfer to queue** contact flow\.

**Contacts transferred out**  <a name="contacts-transferred-out-historical"></a>
Count of contacts transferred from the queue after being answered by an agent\.

**Contacts transferred out external**  <a name="contacts-transferred-out-external-historical"></a>
Count of contacts that an agent transferred from the queue to an external source, such as a phone number other than the phone number for your contact center\.

**Contacts transferred out from queue**  <a name="contacts-transferred-out-from-queue-historical"></a>
Count of contacts transferred from the queue to another queue in a **Transfer to queue** contact flow\.

**Contacts transferred out internal**  <a name="contacts-transferred-out-internal-historical"></a>
Count of contacts for the queue that an agent transferred to an internal source, such as a queue or another agent\. An internal source is any source that can be added as a Quick Connect\.

**Customer hold time**  <a name="customer-hold-time-historical"></a>
Total time that customers spent on hold after being connected to an agent\. This includes time spent on a hold when being transferred, but does not include time spent in a queue\.

**Error status time**  <a name="error-status-time-historical"></a>
Total time that an agent spent in the **Error** status\. This metric can't be grouped or filtered by queue\.

**Maximum queued time**  <a name="maimum-queued-time-historical"></a>
The longest time that a contact spent waiting in the queue\. This includes all contacts added to the queue, even if they were not connected with an agent, such as abandoned contacts\.

**Non\-Productive Time**  <a name="npt-historical"></a>
Total time that agents spent in a custom status \(any status other than **Available**, **Error**, or **Offline**\), including any time they spent handling contacts while in a custom status\. This metric can't be grouped or filtered by queue\.

**Occupancy**  <a name="occupancy-historical"></a>
Percentage of time that agents were active on contacts\. This percentage is calculated as follows:  
\(Agent Handle Time / \(Agent Handle Time \+ Agent Idle Time\)\) \* 100

**Online time**  <a name="online-time-historical"></a>
Total time that an agent spent in a status other than **Offline**\. This includes any time spent in a custom status\. This metric can't be grouped or filtered by queue\.

**Service level *X* seconds**  <a name="service-level-historical"></a>
Percentage of contacts removed from the queue between 0 and *X* seconds after being added to it\. A contact is removed from a queue when the following occurs: an agent answers the contact, the customer abandons the contact, or the customer requests a call back\. The possible values for *X* are: 15, 20, 25, 30, 45, 60, 90, 120, 180, 240, 300, and 600\. This percentage is calculated as follows:  
\(Contacts removed from queue in *X* seconds / Contacts queued\) \* 100
