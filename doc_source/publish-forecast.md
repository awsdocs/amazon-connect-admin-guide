# Publish a forecast<a name="publish-forecast"></a>

When you publish a forecast, you make it visible to other users, such as capacity planners and schedulers, so that they can use the forecasts for capacity planning and scheduling\.

**Important**  
Amazon Connect retains only the last published forecast\. We strongly advise you to download the last published forecast before publishing a new one because the last forecast will be permanently replaced\. For instructions, see [Download last published forecast](#download-last-publish-forecast)\.

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Analytics**, **Forecasting \- View**\. 

   For more information, see [Assign permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Forecasting**\.

1. On the **Forecasts** tab, choose the forecast\. 

1. Choose **Actions**, **Publish forecast**\.

1. Choose the forecasts\.

   The status is **Complete** for successfully published forecasts\. When publish fails, the status is **Publish failed**\.

## Download the last published forecast<a name="download-last-publish-forecast"></a>

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Analytics**, **Forecasting \- View**\. 

   For more information, see [Assign permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Forecasting**\.

1. On the **Forecasts** tab, choose the forecast\. 

1. Choose **Actions**, **Download last published forecast**\.

1. We recommend choosing **click here** as shown in the following image\. This enables you to specify the name of the downloaded file and the location\. Otherwise, the file is saved to your **Downloads** folder and its name is a generated number\.  
![\[The forecast page, the click here link to start the download.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-download-last-published-click-here.png)