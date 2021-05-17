# Save custom reports<a name="save-reports"></a>

You can create custom real\-time, historical, and login/logout reports that include only the metrics you're interested in\. For instructions, see [Create a real\-time metrics report](create-real-time-report.md) and [Create a historical metrics report](create-historical-metrics-report.md)\.

After you create a report, you can: 
+ [Save](#how-to-save-reports) the custom report and return to it later\.
+ [Share](share-reports.md) a link to the custom report so only people in your organization who have the link AND who have the [appropriate permissions](view-a-shared-report.md) in their security profile can access the report\.
+ [Publish](publish-reports.md) the report so everyone in your organization who has the [appropriate permissions](publish-reports.md#view-published-reports) in their security profile can view the report\.

## Personal saved reports count towards quota<a name="personal-saved-reports"></a>

Personal saved reports count towards your service quota of reports per instance\. For example, if you save a report every day, it will count towards your organization's number of saved reports for the instance\. 

For more information about quotas, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

## Create a naming convention<a name="save-reports-naming-convention"></a>

All saved reports in your Amazon Connect instance must have a unique name\. We recommend creating a naming convention that indicates who the owner of the report is\. For example, use the team name or owner alias as the report suffix: Agent Performance \- *team name*\. That way, if the report is published, others will know who owns it\.

If your organization needs to delete reports because you've reached the service quota for reports for your instance, a naming convention that includes the team or owner alias will help you track down the report owners to find out if the report is still needed\. 

## How to save reports<a name="how-to-save-reports"></a>

1. Customize a real\-time, historical, or login/logout report to include the metrics you want\.

1. Choose **Save**\. If you don't have permissions in your security profile to create reports, this button will be inactive\.

1. Assign a unique name to the report\.
**Tip**  
We recommend establishing a naming convention for reports in your organization, especially published reports\. This will help everyone identify who the owner is\. For example, use the team name or owner alias as the report suffix: Agent Performance \- *team name*\.

1. To view to the report at a later time, go to **Metrics and quality**, **Saved reports**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/view-saved-reports.png)

## How to delete saved reports<a name="how-to-delete-saved-reports"></a>

1. On the navigation menu, choose **Metrics and quality**, **Saved reports**\.

1. Choose the **Historical metrics** tab\. 

1. Go to the row that has the report you want to delete, and choose the **Delete** icon\. If you don't have permissions in your security profile to delete reports, this option won't be available\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-delete-saved-report.png)