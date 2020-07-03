# Change the "Agent activity" status in a real\-time metrics report<a name="rtm-change-agent-activity-state"></a>

Agents manually set their status in the Contact Control Panel \(CCP\)\. However, on the real\-time metrics report, supervisors can manually change the **Agent Activity** status of an agent\. This overrides what the agent has set in the CCP\.

When you choose the **Agent Activity** column, you can select a status, such as **Offline**, **Available**, or **Break**\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-change-agent-activity-state.png)

This change appears in the agent event stream\.

You can't select or change any of the contact states that appear in the **Agent Activity** column, such as **Incoming** or **On contact**\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-change-agent-activity-state-incoming.png)

You'll get an error message, as shown in the following image\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-change-agent-activity-state-error-message.png)

## Required permissions to change an agent's activity status<a name="rtm-change-agent-activity-state-permissions"></a>

For someone such as a supervisor to be able to change an agent's activity status, they need to be assigned a security profile that has the following permissions: 
+ Edit/View/Enable/Disable Agent Status
+ Access metrics 
+  View Login/Logout reports

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/security-profile-change-agent-status2.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/security-profile-change-agent-status.png)