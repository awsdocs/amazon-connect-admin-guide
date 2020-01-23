# Publish Reports<a name="publish-reports"></a>

After you create and save a custom report with the metrics you're interested in, you can publish it so everyone in your organization with the [appropriate permissions](#view-published-reports) can access the report\.

After a report is published, people will be able to see the report in their list of Saved reports\.

**Tip**  
We recommend establishing a naming convention for reports in your organization\. When reports are published, this will help everyone identify who the owner is\. For example, use the team name or owner alias as the report suffix: Agent Performance \- *team name*\.

Only people who have permissions in their security profile to **Create** saved reports will be able to change the published report and save their changes to the published version\.

**To publish a report**

1. On the real\-time metrics, historical metrics, login/logout report, or Saved reports page, choose **Share report**\.

1. Toggle **Publish report** to **On**, and then choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/publish-a-report.png)

   The report appears in the list of Saved reports for everyone who has appropriate permissions in their security profile\.

1. To unpublish the report, move the toggle to **Off**\. 

   The report is removed from everyone's list of Saved reports\.

## View Published Reports<a name="view-published-reports"></a>

To view published reports, at minimum you need the following permissions in your security profile:
+  **Access metrics**, if the report is a real\-time or historical metrics report
+  **View** Login/Logout report, if the report is a login/logout report
+  **View** Saved reports  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/permissions-view-saved-metrics-reports.png)

**To view published reports**
+ Go to **Metrics and quality**, **Saved reports**\. 

  Published reports appear in your list automatically\.