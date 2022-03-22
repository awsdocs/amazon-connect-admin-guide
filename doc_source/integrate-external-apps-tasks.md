# Set up applications for task creation<a name="integrate-external-apps-tasks"></a>

You can set up applications for task creation in just a few steps, no coding required\. Amazon Connect uses Amazon EventBridge to pull data from your external application\. 

**Tip**  
If your organization is using custom [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) policies to manage access to the Amazon Connect console, make sure users have the appropriate permissions to set up applications for task creation\. For a list of required permissions, see [Tasks page](security-iam-amazon-connect-permissions.md#tasks-page)\.   
If your instance was created before October 2018, for information about how to configure your service\-linked roles \(SLR\), see [For instances created before October 2018](connect-slr.md#migrate-slr)\.

**Topics**
+ [Set up application integration for Salesforce](integrate-salesforce-tasks.md)
+ [Set up application integration for Zendesk](integrate-zendesk-tasks.md)
+ [Monitor task creation](monitor-task-creation.md)
+ [Disassociate an Amazon Connect connection](disassociate-connection.md)