# Forecasting in Amazon Connect \(Preview\)<a name="forecasting"></a>

Forecasting is the starting point for any scheduling and capacity planning activities\. Before you can generate a schedule or capacity plan, you must create a corresponding forecast\. 

A *forecast* attempts to predict future contact volume and handle time\. We use historical metrics to create the forecast\. 

**Short term forecasts are automatically updated every day**\. When you come into work, you can review the forecast that was updated overnight with the most current data\. You can publish the forecast to make it available to schedulers whenever you want\. The **Forecasting** page displays when a forecast was last updated and published\. Use short term forecasts for scheduling\.

**Long term forecasts are automatically updated every week, based on the day you created the forecast**\. For example, if you created the forecast on a Monday, it is updated every Monday\. Use long term forecasts for hiring\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-lastupdated-date.png)

**Important**  
Only the most current forecast is available\. Because the forecast is updated every day, if you want to keep the current day's forecast, you must download it before Amazon Connect overwrites it\.

## Getting started with forecasting<a name="getting-started-forecasting"></a>

Following is the order of steps for creating a forecast and sharing it with others\.

1. [Set the forecast and scheduling interval](set-forecast-scheduling-interval.md): This is a one\-time activity typically set up by forecasters\. It cannot be undone\.

1. [Create forecast groups](create-forecast-groups.md)

1. [Import historical data](import-data-for-forecasting.md)

1. [Create forecasts](create-forecasts.md)

1. [Inspect a forecast](inspect-forecast.md)

1. [Publish a forecast](publish-forecast.md)

There are other things you can do with a forecast, such as [download to a \.csv file for offline analysis](download-forecasts.md) or [override](override-forecast.md) it, but these steps will get you started\.