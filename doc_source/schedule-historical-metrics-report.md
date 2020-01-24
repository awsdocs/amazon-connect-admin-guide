# Schedule a Historical Metrics Report<a name="schedule-historical-metrics-report"></a>

Before you schedule a historical metrics report, here are a few things you need to know:

**Others Can Access the Report**
+ Scheduling a report makes the report accessible by any other users in your contact center who have permissions to view saved reports\. Any user with permission to edit saved reports can also modify your scheduled reports\. 

**Scheduled Reports are Located in an Amazon S3 Bucket**
+ Scheduled reports are saved as CSV files in the Amazon S3 bucket specified for reports for your contact center\. When you set up the scheduled report, you can add a prefix to the location in Amazon S3 for the report files\.
+ When the report is exported to your Amazon S3 bucket, the file name includes the date and UTC time when the report was created\. The **Last modified date** for the file is displayed using the time zone for the Amazon S3 bucket, and may not match the creation time for the report, which is in UTC\.

**There's a 15 Minute Delay**
+ For scheduled reports, there is a delay of 15 minutes after the scheduled report time before the report is generated\. This is to ensure that the report includes the data for all of the activity that occurred during the time range specified for the report\. Data from your contact center is not immediately processed and available to include in reports, so some data from the time range might not be captured in a report if the report is generated at the second the time range ends\. 
+ For example, if you create a scheduled report for time frame of 8:00 AM to 5:00 PM, and there is activity in your contact center between 4:46:00 PM and 4:59:59 PM, the data about that activity may not be aggregated prior 5:00 PM when the report is scheduled to generate\. Instead, the report is generated after 5:15 PM, by which time the data for the last 15 minutes of the time range is included in the report\.

**A Scheduled Yesterday Report Works Like a Last 24 Hours Report**
+ Usually **Yesterday** specifies the previous calendar day while **Last 24 hours** specifies the 24 hours prior to the current time\. However, if you schedule to run a **Yesterday** report, it will work like a **Last 24 hours** report\.

**No Message if a Scheduled Report Doesn't Run**
+ If a scheduled report fails to run, you won't get any message in the Amazon Connect UI\. You just won't see the report in the Amazon S3 location\. 

## How to Schedule a Historical Metrics Report<a name="w37aac42c35c17c15"></a>

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Create a new report and save it, or open a saved report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Schedule**\.

1. On the **Recurrence** tab, specify how often this report should be run \(for example, weekly on Saturdays\) and the range \(for example, from midnight for the previous 5 days\)\.

1. \(Optional\) On the **Delivery Options** tab, specify a prefix for the location in Amazon S3 for the report files\.

1. Choose **Create**\.