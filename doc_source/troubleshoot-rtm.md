# No Metrics or Too Few Rows in a Queues Report?<a name="troubleshoot-rtm"></a>

It's possible to run a manually configured queues report and have no metrics returned, or fewer rows than expected\. 

This is because a queues report only includes data for a maximum of 100 queues, using one row per queue\. If a queue doesn't have any activity\* during the time range for the report, it's excluded from the report rather than included with null values\. This means that if you create a report, and there is no activity for any of the queues included in the report, your report will not include any data\.

**Tip**  
\*Here's how we define whether a queue is active: there's at least one contact in queue or there's at least one online agent for that queue\. Otherwise, it’s considered inactive\.

In the following situations, you could end up with no metrics or fewer rows than expected:

1. You're attempting to run a report with no filters or groupings, and have more than 100 queues in your instance\. The report pulls metrics for the first 100 queues, and then displays only those that are active\. 

1. You're attempting to run a report with filters and groupings, but it still has more than 100 queues matching that criteria\. To process this request, Amazon Connect applies all the specified filters and groupings\. This pulls the first 100 queues matching that criteria\. Then out of those queues, it displays only the active ones\. 

   For example, let’s say you have 300 queues in your instance\. Of these, 200 match your criteria; 100 are active and by coincidence all happen to be Queues \#100\-\#200\. When you run the report, you'd get just 1 row \(Queue \#100\) since the other 99 queues that were returned \(Queues \#1\-\#99\) were considered inactive and were not displayed\.

1. You're running a report with fewer than 100 queues\. While you may expect to see metrics for all filtered queues, only active queues are shown on the real\-time metrics report page\. Try changing the settings for the report, such as changing the time range\. 