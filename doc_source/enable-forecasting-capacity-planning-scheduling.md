# Enable forecasting, capacity planning, and scheduling<a name="enable-forecasting-capacity-planning-scheduling"></a>

You enable forecasting, capacity planning, and scheduling at the Amazon Connect instance level\.

**Requirements**

The user must have the following permissions:
+ `iam:CreateRole`
+ `iam:CreatePolicy`
+ `iam:AttachRolePolicy`
+ `bayes-markov:*`

**To enable forecasting, capacity planning, and scheduling**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.

1. In the navigation pane, choose **Forecasting, capacity planning, and scheduling**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-enable-console.png)

1. On the **Forecasting, capacity planning, and scheduling** page, choose **Enable Forecasting, capacity planning, and scheduling**\. 

   Your users will have access to forecasting, capacity planning, and scheduling within 24 hours\. After forecasting, capacity planning, and scheduling capabilities are enabled, continue setup as follows: 

   1. Assign users the appropriate security profile permissions to access the features\. For instructions, see [Required permissions](required-optimization-permissions.md)\.

   1. [Set the forecast and scheduling interval](set-forecast-scheduling-interval.md)\. This is a one\-time activity typically done by forecasters\. After it's set, it cannot be undone\. 