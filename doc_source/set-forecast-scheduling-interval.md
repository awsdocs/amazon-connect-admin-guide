# Set the forecast and schedule interval<a name="set-forecast-scheduling-interval"></a>

You can set the granularity for your short\-term forecasts and your schedules\.

**Important things to know**
+ You must have security profile permissions for **Analytics**, **Forecast and schedule interval \- Edit**\. For more information, see [Security profile permissions for Forecasting, capacity planning, and scheduling](required-optimization-permissions.md)\.
+ You must specify an interval for short\-term forecasting and scheduling\.
+ Amazon Connect supports 15\- or 30\-minute intervals\. For example, if you select 30 minutes as the interval, your short\-term forecasts are generated for 30\-minute intervals \(that is, 20 contacts between 9:00 AM\-9:30 AM\), and your schedules are computed for 30 minute intervals\.
+ You must set up a forecast and a schedule interval before you can generate forecasts or create forecast groups\. 
+ After you set the forecast and schedule interval, you cannot change it\.

**To set the forecast and schedule interval**

1. Log in to the Amazon Connect console\.

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Forecasting**\.

1. Choose the **Forecast and schedule interval** tab\. You'll see this tab only if you have the appropriate security profile permissions\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecast-schedule-interval.png)

1. Choose one of the following options:
   + **15 minute interval** – Generates short\-term forecasts in 15\-minute intervals\. For example, 20 contacts between 9:00 AM to 9:15 AM, and 30 contacts between 9:15 AM to 9:30 AM\.
   + **30 minute interval** – Generates short\-term forecasts in 30\-minute intervals\. For example, 20 contacts between 9:00 AM to 9:30 AM, 30 contacts between 9:30 AM to 10:00 AM\.