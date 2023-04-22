# Create forecasts<a name="create-forecasts"></a>

Forecasts are a projection of the workload in your contact center\. Amazon Connect provides long\-term and short\-term forecasts for you to generate capacity plans and agent schedules\. The forecasts include inbound, transfer, and callback contacts in both voice and chat channels\.

After creating a forecast, you will not need to generate it manually\.
+ Short\-term forecasts are scheduled to run automatically every day\.
+ Long\-term forecasts are automatically updated every week, based on the day you created the forecast\. For example, if you created the forecast on a Monday, it is updated every Monday\.
+ Every forecast is computed using the most current contact data\.
+ The models for short\-term and long\-term forecasts are retrained on a weekly and monthly basis respectively to incorporate the latest contact pattern\.
+ You can delete forecasts\. Downstream capacity plans and schedules created based on the forecasts will be impacted\.

**To create a forecast**

1. Before creating a forecast, you must create at least one forecast group\. If you haven't yet done that, see [Create forecast groups](create-forecast-groups.md)\. We strongly recommend creating all of your forecast groups before creating any forecast\.

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Analytics**, **Forecasting \- Edit**\. 

   For more information, see [Assign permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Forecasting**\.

1. Select the **Forecast** tab, and then choose **Create Forecast**\.

1. On the **Create Forecast** page, choose the forecast groups\.  
![\[The Create forecast page, the forecast groups dropdown menu.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-create-forecast.png)

1. Choose the forecast type\. Amazon Connect creates a forecast for each type you select\.
   + **Long term** forecasts are used for capacity planning\. For example, how many Full Time Equivalent \(FTE\) agents you need to hire in the next few months, quarter, and year\.
   + **Short term** forecasts are used for scheduling agents and interval level agent headcount estimation\. 

1. Choose **Save**\. If the forecast group has already been included in a forecast, an error message is displayed\. 

1. If the forecast was created successfully, it's Status = **Scheduled**\. 

    The status is **Complete** when the computation finishes\. You can use **Search** to find forecasts by forecast group name\.

1. Amazon Connect creates a forecast for each forecast type, as shown in the following image\.  
![\[A list of forecasts, short term and long term.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-types.png)