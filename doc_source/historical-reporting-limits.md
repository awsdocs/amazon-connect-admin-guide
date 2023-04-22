# Historical report limits<a name="historical-reporting-limits"></a>

Historical metrics reports have the following limits:

**Service quotas**
+ Historical metrics reports have service quotas, such as **Reports per instance** and **Scheduled reports per instance**\. When service quotas are breached, the following error message is displayed: *Report cannot be saved*\. For more information about these quotas, see [Amazon Connect service quotas](amazon-connect-service-limits.md)

**Data only for active queues**
+ You can get data only for active queues\. A queue is inactive if there are no contacts in the queue and no agents available\.

**Query data for three days at a time, for the past 35 days**
+ When you create a report that uses 15 minute intervals, you can return data for three days at a time, for the past 35 days\. For 30 minute intervals you can return data for only three days at a time, but the data is available based on the retention period of contact records\. 

**The availability of historical metric data is based on the retention period of contact records**
+ Historical metrics are based contact records\. For the current retention period for contact records, see [Amazon Connect feature specifications](feature-limits.md)\.

**For daily and total intervals**
+ You can select up to 31 days in a single request\.

**80k cell limit**

There is currently an 80k cell limitation on historical metrics reports and scheduled reports\. This applies to the total number of cells \(columns \* rows\), accounting for grouping and filtering\. 

For example, let's say you create a historical metrics report with this criteria: 
+ Grouped by agents
+ With an interval of 30 minutes
+ For the last 24 hours
+ Configured to include only 5 metrics
+ Filtered to show only contacts handled in BasicQueue

If only 10 agents handled contacts in BasicQueue during this time, then you would expect to see \(24\*2\)\*5\*10 = 2400 cells that count towards the 80k limit\.

A message informs you if you reach the limit\. 