# Historical report limits<a name="historical-reporting-limits"></a>

Historical metrics reports have the following limits:

**Data only for active queues**
+ You can get data only for active queues\. A queue is inactive if there are no contacts in the queue and no agents available\.

**Query data for three days at a time, for the past 35 days**
+ When you create a report that uses intervals \(such as 30 minute intervals\), you can return data for three days at a time, for the past 35 days\.

**The availability of historical metric data is based on the retention period of CTRs**
+ Historical metrics are based CTRs\. For the current retention period for CTRs, see [Feature specifications](amazon-connect-service-limits.md#feature-limits)\.

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