# Download a historical metrics report<a name="download-historical-metrics-report"></a>

You can download the data included in a report as a comma\-separated value \(CSV\) file so you can use it with other applications\. If there's no data for one of the selected metrics, the field in the downloaded CSV file contains a dash\.

**To download a historical metrics report as a CSV file**

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.

1. Create a new report or open a saved report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Download CSV**\.

1. When prompted, confirm whether to open or save the file\.

Although the times in the online report are in hh:mm:ss, all times in the downloaded report are in seconds\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/example-downloaded-metrics-report.png)

You can convert the seconds to minutes using an Excel formula\. Alternatively, if you have a short report, you can copy and paste the data from Amazon Connect to Excel and it will preserve the format\.

## Interval downloaded in ISO date format<a name="interval"></a>

The interval is downloaded in ISO date format, as shown in the following image\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/downloaded-hmr-interval-format.png)

## Download all historical metric results<a name="download-all-historical-metrics"></a>

If you need to download more than a page or two of historical metrics, we recommend using the following steps:

1. Schedule the report to run as often as needed\.

   For example, you might schedule the Login/Logout report to run daily at midnight\.

1. The full report is saved to your Amazon S3 bucket\.

1. Go to your Amazon S3 bucket and download the report\.

To learn how scheduled reports work, see [Schedule a historical metrics report](schedule-historical-metrics-report.md)\. 