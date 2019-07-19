# Customize Agent Status Values<a name="agent-status"></a>

Agent states appear to the agents in the contact control panel \(CCP\)\. These states are also used for reporting, metrics, and resource management\.

 Amazon Connect provides two default states: 
+ Available
+ Offline

You can change the name of these states, and you can add new states\. For example, you might add states for Break, and another for Training\.

You can't delete a status but you can disable it so it doesn't appear on the agent's contact control panel \(CCP\)\.

**To add a new agent status**

1. Choose **Users, Agent status**, **Add new agent status**\.

1. Enter a status name, description, and type, and select whether the status should appear in the CCP to the agent\.

1. Choose **Save**\.

To change the order that the states appear in the CCP, click the waffle next to the state and drag it to the order you want\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-status.png)

**To edit a status**

1. Choose **Users**, **Agent status**\.

1. Hover over the status name and choose the edit icon\.

1. Enter the new information, and choose **Save** to apply the changes\.

Choose **View Historical Changes** to view the change history\. You can filter changes by date \(between two dates\) or by user name\. If you cannot see the **View historical changes** link, ensure that you have the proper permissions to view these changes\.