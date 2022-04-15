# Create forecast groups \(Preview\)<a name="create-forecast-groups"></a>

Forecast groups are a way for you to combine different queues into one forecast\. This enables you to create a forecast from aggregated data from multiple queues, instead of from just one queue\. 

## Important things to know<a name="important-things-create-forecast-groups"></a>
+ Forecast groups are associated with a staffing group for scheduling purposes\. Therefore, we recommend you group queues that share the same pool of staff \(agents\) under the same forecast group\. It enables you to generate a more accurate forecast\.
+ Each queue can belong to only one forecast group\. This prevents duplicates in the forecast\. 
+ You must create at least one forecast group before you can generate any forecast\. 
+ We strongly recommend that you create all forecast groups before creating any forecast\. 

  Amazon Connect uses historical data for queues included in all forecast groups to train your forecasting model\. By creating forecasts after all forecast groups are created, you ensure historical data of all relevant queues are included in the training\.
+ If a queue is associated with a forecast group and is later disabled, it does not change the forecast group\. The queue will still be included by the forecast group and the historical data associated with it will be included in the forecast\. Over time, because no contact reaches the disabled queue, it stops impacting the forecast\.

## How to create forecast groups<a name="howto-create-forecast-groups"></a>

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Analytics**, **Forecasting \- Edit**\. 

   For more information, see [Required permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics**, **Forecasting**\.

1. Select the **Forecast groups** tab, and then choose **Create forecast group**\.

1. On the **Create Forecast Groups** page, under **Queues**, you'll see a list of queues that are not yet associated with a forecast group are listed\. If no queues are listed, it means they are all associated with a forecast group already\.

1. Drag and drop one or more queues to the forecast group\. You can press and hold CTRL \(COMMAND for macOS users\) or SHIFT to select multiple queues at a time\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-drag-drop-queues-to-forecast-group.png)

1. Choose **Save**\. The new forecasting group appears, along with the number of queues in the group and the date it was last changed\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-forecasting-group.png)

1. After creating a forecast group, you can add or remove queues\. However, doing so might initiate an immediate change in associated forecasts\. It will also impact downstream capacity plans and schedules that are created based on the forecast group\.

## Next steps<a name="nextsteps-create-forecast-groups"></a>

Now you're ready to create a forecast\. For instructions, see [Create forecasts](create-forecasts.md)\.