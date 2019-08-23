# Historical Metrics Reports<a name="historical-metrics"></a>

Historical metrics reports include data about past, completed activity and performance in your contact center\. You can customize the report settings to get the view of the data that is most meaningful for your organization\. You can change the time frame for the report, which metrics are included in the report, and how data is grouped in the report\. After you have customized a report, you can save it for future reference\. You can generate a report using a recurring schedule that you define\.

Historical metrics have two categories:
+  CTR driven metrics, like **Service level**, **Agent interaction time**, **Customer hold time**, **After contact work time**, **Contact Handle time**, etc\. 

  These metrics are based on formed CTR records\. For a given interval, CTRs whose disconnect date falls in the interval are selected to calculate metrics\. For example, if a contact starts at 05:23 and ends at 06:15, this contact contributes 52 minutes of metrics for the 06:00\-06:30 interval\. 
+ Agent activity driven metrics, like **Agent on contact time**, **Online time**, **Agent idle time**, **Non\-Productive Time**, etc\. 

  These metrics are based on agent activities, like agent status changes, agent conversation changes\. The metrics reflect on the actual time the activity happens\. For example, if agent handles a contact from 05:23 to 06:15, the **Agent on contact time** will have 7 minutes for the 05:00\-05:30 interval, 30 minutes for the 05:30\-06:00 interval, and 15 minutes for the 06:00\-06:30 interval\.

**Topics**
+ [Create a Historical Metrics Report](create-historical-metrics-report.md)
+ [Report Limits](historical-reporting-limits.md)
+ [Schedule a Historical Metrics Report](schedule-historical-metrics-report.md)
+ [Update a Historical Metrics Report](update-historical-metrics-report.md)
+ [Download a Historical Metrics Report](download-historical-metrics-report.md)
+ [Historical Metrics Definitions](historical-metrics-definitions.md)