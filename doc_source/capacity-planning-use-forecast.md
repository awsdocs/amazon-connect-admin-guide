# Create capacity plans using forecasts and scenarios<a name="capacity-planning-use-forecast"></a>

Before you can create a capacity plan, you must create a planning scenario and publish a long\-term forecast\. Amazon Connect uses the forecasts and planning scenarios as inputs for creating the capacity plan\. If you haven't yet created a forecast and planning scenario, see [Getting started with forecasting](forecasting.md#getting-started-forecasting) and [Create capacity planning scenarios](capacity-planning-create-scenarios.md)\. 

## How to create a capacity plan<a name="how-to-create-capacity-plan"></a>

1. Go to the **Capacity Plans** tab, and choose **Generate Plan**\.

1. Provide the plan name, description, forecast group \(which has published long\-term forecasts\), start/end date, and plan scenario\. See the following image for an example:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-capacity-planning-create-plan.png)

1. Choose **Generate Capacity Plan**\.

1. To quickly identify the plan that is in processing, choose **Last Computed** to sort the table list\. In the following example, the status of the plan is **In Progress**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-capacity-planning-in-progress.png)

   It usually takes between 5\-10 minutes for the plan to be generated\. If the plan generation fails, try publishing the selected long\-term forecasts, and then generating the capacity plan again\.