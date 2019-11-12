# Customize Agent Status Values<a name="agent-status"></a>

The agent's status is set manually in the Contact Control Panel \(CCP\)\. The status is used for reporting, metrics, and resource management\.

Amazon Connect provides two default statuses: 
+ Available
+ Offline

You can change the name of these statuses, and you can add new statuses\. For example, you might add a status for Break, and another for Training\.

When you add a new status, it will always be **Custom**, not routable\. 

You can't delete a status but you can disable it so it doesn't appear on the agent's CCP\.

**To add a new agent status**

1. Choose **Users, Agent status**, **Add new agent status**\.

1. Enter a status name and description, and select whether the status should appear in the CCP to the agent\.

1. Choose **Save**\.

To change the order that the statuses appear in the CCP, click the waffle next to the state and drag it to the order you want\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-status.png)

**To edit a status**

1. Choose **Users**, **Agent status**\.

1. Hover over the status name and choose the edit icon\.

1. Enter the new information, and choose **Save** to apply the changes\.

Choose **View Historical Changes** to view the change history\. You can filter changes by date \(between two dates\) or by user name\. If you cannot see the **View historical changes** link, ensure that you have the proper permissions to view these changes\.