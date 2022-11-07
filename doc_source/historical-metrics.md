# Historical metrics reports<a name="historical-metrics"></a>

Historical metrics reports include data about past, completed activity and performance in your contact center\. Amazon Connect includes built\-in historical reports that you can start using right away\. You can also build your own custom reports\. 

When creating and analyzing your historical metrics reports, keep in mind that there are two categories of metrics:

**Contact record\-driven metrics**  <a name="ctr-driven-metrics"></a>
These metrics are based on formed contact record records\. For a given interval, contact records whose disconnect date falls in the interval are selected to calculate metrics\. For example, if a contact starts at 05:23 and ends at 06:15, this contact contributes 52 minutes of metrics for the 06:00\-06:30 interval\.   
Example contact record\-driven metrics are **Service level**, **Agent interaction time**, and **After contact work time**\. 

**Agent activity\-driven metrics**  <a name="termdef"></a>
These metrics are based on agent activities, like agent status changes, agent conversation changes\. The metrics reflect on the actual time the activity happens\. For example, if agent handles a contact from 05:23 to 06:15, the **Agent on contact time** has 7 minutes for the 05:00\-05:30 interval, 30 minutes for the 05:30\-06:00 interval, and 15 minutes for the 06:00\-06:30 interval\.  
For example, an agent activity\-driven metric is **Non\-Productive Time**\. 

You can customize the report settings to get the view of the data that is most meaningful for your organization\. You can change the time frame for the report, which metrics are included in the report, and how data is grouped in the report\. After you have customized a report, you can save it for future reference\. You can generate a report using a recurring schedule that you define\.

**Topics**
+ [Historical metrics definitions](historical-metrics-definitions.md)
+ [Permissions required to view historical metrics reports](htm-permissions.md)
+ [Create a historical metrics report](create-historical-metrics-report.md)
+ [Historical report limits](historical-reporting-limits.md)
+ [Schedule a historical metrics report](schedule-historical-metrics-report.md)
+ [Update a historical metrics report](update-historical-metrics-report.md)
+ [Download a historical metrics report](download-historical-metrics-report.md)
+ [Show agent queues in a Queues table](show-agent-queues.md)
+ [How many contacts in queue on a specific date](contacts-in-queue-on-specific-date.md)
+ [Agent activity audit report](agent-activity-audit-report.md)