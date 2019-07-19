# Create a Real\-time Metrics Report<a name="create-real-time-report"></a>

You can create a real\-time metrics report to view real\-time or near\-real time metrics data for activity in your contact center\. You must have permission to access metric data\. The **CallCenterManager** and **QualityAnalyst** security profiles include this permission\. For more information, see [Assign Permissions: Security Profiles](connect-security-profiles.md)\.

**To create a real\-time metrics report**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Metrics and Quality**, **Real\-time metrics**\.

1. Choose one of the following report types, which group and order the data in different ways and include different metrics by default:
   + **Queues**
   + **Agents**
   + **Routing profiles**

1. To add a another report to the page, choose **New table** and then choose a report type\. You can add multiple reports of the same report type\.

1. To customize a report, choose the gear icon from its table\.

1. On the **Time Range** tab, do the following:

   1. For **Trailing windows for time**, select the time range, in hours, for the data to include in the report\.

   1. \(Optional\) If you select **Midnight to now**, the time range is from midnight to the current time, based on the **Time Zone** that you select\. If you select a time zone other than the one you are currently in, the time range starts at midnight for the calendar day in that time zone, not your current time zone\.

1. \(Optional\) On the **Filters** tab, specify filters to scope the data to be included in the report\. The available filters depend on the report type\. The following are the possible filters:
   + **Agents**—Includes data only for the agents that you select from **Include**\.
   + **Agent Hierarchies**—Includes data only for the agent hierarchies that you select from **Include**\.
   + **Queues**—Includes data only for the queues that you select from **Include**\.
   + **Routing profiles**—Includes data only for the routing profiles that you select from **Include**\.

1. On the **Metrics** tab, choose the metrics and fields to include in the report\. The available metrics and fields depend on the report type and filters that you select\. For more information, see [Real\-time Metrics Definitions](real-time-metrics-definitions.md)\.

1. When you are finished customizing the report, choose **Apply**\.

1. \(Optional\) To save your report for future reference, choose **Save**, provide a name for the report, and then choose **Save**\.

   To view your saved real\-time metrics reports, choose **Metrics and Quality**, **Saved reports**, and then choose the **Real\-time metrics** tab\.