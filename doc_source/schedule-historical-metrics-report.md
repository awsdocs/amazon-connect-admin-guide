# Schedule a historical metrics report<a name="schedule-historical-metrics-report"></a>

Before you schedule a historical metrics report, here are a few things you need to know:

**Others can access the report**
+ Scheduling a report makes the report accessible by any other users in your contact center who have permissions to view saved reports\. 

**Anyone with Schedule permissions can create, edit, or delete the schedule of your report**
+ After you publish a report, any user with **Saved reports \- Schedule** permissions in their security profile can create, edit, or delete the schedule of your report\. They cannot delete the actual report\.

**Scheduled reports are located in an Amazon S3 bucket**
+ Scheduled reports are saved as CSV files in the Amazon S3 bucket specified for reports for your contact center\. When you set up the scheduled report, you can add a prefix to the location in Amazon S3 for the report files\.
+ When the report is exported to your Amazon S3 bucket, the file name includes the date and UTC time when the report was created\. The **Last modified date** for the file is displayed using the time zone for the Amazon S3 bucket, and may not match the creation time for the report, which is in UTC\.

**There's a 15 minute delay**
+ For scheduled reports, there is a delay of 15 minutes after the scheduled report time before the report is generated\. This is to ensure that the report includes the data for all of the activity that occurred during the time range specified for the report\. Data from your contact center is not immediately processed and available to include in reports, so some data from the time range might not be captured in a report if the report is generated at the second the time range ends\. 
+ For example, if you create a scheduled report for time frame of 8:00 AM to 5:00 PM, and there is activity in your contact center between 4:46:00 PM and 4:59:59 PM, the data about that activity may not be aggregated prior 5:00 PM when the report is scheduled to generate\. Instead, the report is generated after 5:15 PM, by which time the data for the last 15 minutes of the time range is included in the report\.

**A scheduled Yesterday report works like a Last 24 hours report**
+ Usually **Yesterday** specifies the previous calendar day while **Last 24 hours** specifies the 24 hours prior to the current time\. However, if you schedule to run a **Yesterday** report, it will work like a **Last 24 hours** report\.

**All scheduled reports use the UTC day, regardless of the timezone of the report**
+ For example, let's say you are in PST \(Pacific Standard Time\) and you schedule a **Last 24 hours** report to run at 16:00 every day\. Here's the logic we use to run the report on May 15, 2020, for example:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/schedule-historical-metrics-report.html)

**No message if a scheduled report doesn't run**
+ If a scheduled report fails to run, you won't get any message in the Amazon Connect UI\. You just won't see the report in the Amazon S3 location\. 

**Use your messaging system to email scheduled reports**
+ To email a scheduled report to a list of co\-workers, you need to generate the email manually using your messaging system\. Amazon Connect doesn’t provide an option to email the scheduled report automatically\. 

## How to schedule a historical metrics report<a name="howto-schedule-historical-metrics-report"></a>

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.

1. Create a new report and save it, or open a saved report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Schedule**\.

1. On the **Recurrence** tab, specify how often this report should be run \(for example, weekly on Saturdays\) and the range \(for example, from midnight for the previous 5 days\)\.

1. \(Optional\) On the **Delivery Options** tab, specify a prefix for the location in Amazon S3 for the report files\.

1. Choose **Create**\.

## How to delete a scheduled report<a name="howto-delete-scheduled-report"></a>

To get to the page where you can delete a scheduled report, you need to create another temporary scheduled report\.

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.

1. On the navigation menu, choose **Analytics and optimization**, **Saved reports**\. 

1. On the **View reports** page, choose the **Historical metrics** tab\.

1. Click or tap on the saved report that has been scheduled\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Schedule**\.

1. Choose **Create**\. 

1. On the **Schedule Report** page, choose **Delete** next to the scheduled reports you want to delete\. 

For instructions on deleting saved reports, see [How to delete saved reports](save-reports.md#how-to-delete-saved-reports)\.