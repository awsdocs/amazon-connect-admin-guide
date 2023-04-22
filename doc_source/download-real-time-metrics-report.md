# Download a real\-time metrics report<a name="download-real-time-metrics-report"></a>

You can download the data included in your report as a comma\-separated value \(CSV\) file so that you can use it with other applications\. If there is no data for one of the selected metrics, the field in the downloaded CSV file contains a dash\.

All exported times are in seconds\.

**To download a real\-time metrics report as a CSV file**

1. Create the report\.

1. Choose the down arrow next to **Save** in the top\-right corner of the page and choose **Download CSV**\.

1. When prompted, confirm whether to open or save the file\.

The following image shows real\-time metrics in a Queue table\. All times in the online report are in hours:minutes:seconds \(hh:mm:ss\)\. Below the image of the Queue table, there is an image of the same data in a downloaded CSV file opened with Excel\. All times in the downloaded report are in seconds\.

![\[Data in a queue table and the same data in a CSV file.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/example-downloaded-metrics-report.png)

You can convert the seconds to minutes using an Excel formula\. Alternatively, if you have a short report, you can copy and paste the data from Amazon Connect to Excel and it will preserve the format\.