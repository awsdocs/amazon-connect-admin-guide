# Historical report limits<a name="historical-reporting-limits"></a>

Historical metrics reports have the following limits:

**Data only for active queues**
+ You can get data only for active queues\. A queue is inactive if there are no contacts in the queue and no agents available\.

**Download data limited to current page max \(100 results\)**
+ When you want to download historical metrics data into a \.csv file from the user interface, you can only download the data displayed on the page at any one time\. For example, if you have 256 records you want to download, and the maximum displayed in the user interface is 100, you would have to download the data three batches:
  + 1\-100
  + 101\-200
  + 201\-256

  For a workaround so you can download hundreds or thousands of results, see [Download all historical metric results](download-historical-metrics-report.md#download-all-historical-metrics)\.

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