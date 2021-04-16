# Add custom agent status<a name="agent-custom"></a>

Agents are responsible for setting their status in the Contact Control Panel \(CCP\)\. In fact, the only time an agent's status changes is when they manually change it in the CCP, or when [their supervisor changes it](rtm-change-agent-activity-state.md) in a real\-time metrics report\. 

Amazon Connect provides two default status values: 
+ Available
+ Offline

You can change the name of these values, and you can add new ones\. For example, you might add a status for Lunch, and another for Training\. These and the default status values will be used for reporting, metrics, and resource management\. 

When you add a new status, it will always be **Custom**, not routable\. 

You can't delete a status value but you can disable it so it doesn't appear on the agent's CCP\.

**To add a new agent status**

1. Choose **Users, Agent status**, **Add new agent status**\.

1. Enter a status name and description, and select whether the status should appear in the CCP to the agent\.

1. Choose **Save**\.

To change the order that the status values appear in the CCP, click the waffle next to the status value and drag it to the order you want\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-status.png)

**To edit a status**

1. Choose **Users**, **Agent status**\.

1. Hover over the status name and choose the edit icon\.

1. Enter the new information, and choose **Save** to apply the changes\.

Choose **View Historical Changes** to view the change history\. You can filter changes by date \(between two dates\) or by user name\. If you can't see the **View historical changes** link, make sure you have permissions to view these changes\.