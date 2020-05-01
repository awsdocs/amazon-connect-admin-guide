# Download a Historical Metrics Report<a name="download-historical-metrics-report"></a>

You can download the data included in a report as a comma\-separated value \(CSV\) file so you can use it with other applications\. If there's no data for one of the selected metrics, the field in the downloaded CSV file contains a dash\.

**Important**  
From the Amazon Connect console, you can only download the results currently displayed on the page\. For example, if there are 256 results, but only 100 are displayed on the page at a time, you would need to download the data in three batches \(1\-100, 101\-200, 201\-256\)\. For a workaround, see [Download All Historical Metric Results](#download-all-historical-metrics)\. 

**To download a historical metrics report as a CSV file**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Create a new report or open a saved report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Download CSV**\.

1. When prompted, confirm whether to open or save the file\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/downloaded-hmr-interval-format.png)

## Download All Historical Metric Results<a name="download-all-historical-metrics"></a>

If you need to download more than a page or two of historical metrics, we recommend using the following steps:

1. Schedule the report to run as often as needed\.

   For example, you might schedule the Login/Logout report to run daily at midnight\.

1. The full report is saved to your Amazon S3 bucket\.

1. Go to your Amazon S3 bucket and download the report\.

To learn how scheduled reports work, see [Schedule a Historical Metrics Report](schedule-historical-metrics-report.md)\. 