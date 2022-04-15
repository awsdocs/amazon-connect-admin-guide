# Inspect a forecast \(Preview\)<a name="inspect-forecast"></a>

You can inspect your forecasts before publishing them\. You can do this in the online user interface, or [download the forecasts](download-forecasts.md) for offline analysis\.

To help make it easier to inspect a forecast in the user interface, the forecast data is displayed in both a graph and a table\. Use the controls on the report settings panel and calendar picker to adjust and filter the data for a more granular view\. For example, you can:
+ Use the calendar to change the horizon\. You can zoom into specific dates\.
+ Choose 15 minute intervals if your date range is less than a week\. This enables you to see the exact contact pattern of the day\.
+ Compare **Last computed forecast** and **Last published forecast** as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-compare-last-published.png)

  Choose the **Override** setting to inspect the effect of any override you uploaded\. The **Override** option is active only after an override has been uploaded\. For more information, see [Override a forecast](override-forecast.md)\.

  In the table, you can see the original value that you overrode\. Hover over the blue triangle\. It shows the original value that was overwritten\. For example, in the following image, the original value is 72\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-override-original-value.png)
+ Filter by queues or channels to limit your forecast to one or more type\.