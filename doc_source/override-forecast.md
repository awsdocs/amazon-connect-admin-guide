# Override a forecast<a name="override-forecast"></a>

You can override the forecast at the queue channel level by uploading a \.csv file\. Override allows you to modify forecasts and make sure the forecasts reflect the contact pattern in special events \(for example, a one\-off marketing event that can increase volume by 10 percent in a given week\)\.

You can also remove the override if the override is no longer applicable\.

## Important things to know<a name="important-things-to-know-override-forecast"></a>
+ To override a forecast, you need to prepare and upload a \.csv file with your override data\. Currently Amazon Connect does not support changing the values in forecasting user interface directly\.
+ The override data file be must a \.csv file and it must be in the required format\. If the file format and data don't meet the requirements, the upload does not work\. We recommend downloading and using the template provided to help you prepare the historical data\. 

  The following image shows an example csv file with data in it\.   
![\[CSV file opened in Excel, historical data that is properly formatted.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-override-table.png)

  Following are the requirements for imported data: 
  + `QueueName`: Enter the Amazon Connect queue name\.
  + `QueueId`: Enter the Amazon Connect queue ID\. To find the queue ID in the Amazon Connect console, on the left navigation, go to **Routing**, **Queues**, choose the queue, select **Show additional queue information**\. The queue ID is the last number after `/queue/`\.
  + `ChannelType`: Enter `CHAT` or `VOICE`\.
  + `TimeStamp`: Enter the timestamp in UTC \(ISO8601\) format\.
  + `IntervalDuration`: Enter `15mins` or `30mins` for short\-term forecast, depending on your forecast and schedule interval\. Enter `daily` for long\-term forecast\.
  + `IncomingContactVolume`: Enter the number of inbound, transfer, and callback contacts as an integer\.
  + `AverageHandleTime`: Enter the amount of average handle time \(in seconds\) as type double/decimal\.
+ You can upload only one override file for a forecast group\.
  + This means if you previously uploaded an override file \(for example, with 120 lines of overrides\), you must add new overrides to this override file \(for example, add 50 new lines of overrides\) and re\-upload the file that now has 170 lines of overrides\. 
  + This also means you will need to include overrides for both short\-term and long\-term forecasts in one file\.
+ Both contact volume and Average Handle Time metrics are included in one override file\. Both columns must be populated in the override file\. 
+ The following special characters are allowed in the \.csv file: \-, \_, \., \(, and \)\. Space is allowed\.

## How to override a forecast<a name="howto-override-forecast"></a>

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Analytics**, **Forecasting \- Edit**\. 

   For more information, see [Assign permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Forecasting**, and then choose the **Forecast** tab\.

1. Choose the forecast\.

1. Choose **Actions**, **Upload forecast override**\.

1. Choose **Download the CSV template for override data**\.
**Note**  
Amazon Connect supports one, which would be the latest, override file per forecast group\.   
If you have never uploaded an override file, your template will contain headings but no data\.
 If you have uploaded override file in the past, your template will be the previously uploaded file\.

   If you need to make changes later on to the same forecast, you must download the last uploaded file, make your changes, and then upload the file\. Amazon Connect retains only the last uploaded file\.

1. Add override data, and then choose **Upload file** to upload it\. Choose **Apply** to confirm forecast override\.