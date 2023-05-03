# Assign permissions to monitor live conversations<a name="monitor-conversations-permissions"></a>

For managers to monitor live conversations, you assign them the **CallCenterManager** and **Agent** security profiles\. To allow agent trainees to monitor live conversations, you may want to create a security profile specific for this purpose\.

**To assign a manager permissions to monitor a live conversation**

1. Go to **Users**, **User management**, choose the manager, and then choose **Edit**\.

1. In the Security Profiles box, assign the manager to the **CallCenterManager** security profile\. This security profile also includes a setting that makes the icon to download recordings appear in the results of the **Contact search** page\. 

1. Assign the manager to the **Agent** security profile so they can access the Contact Control Panel \(CCP\), and use it to monitor the conversation\.

1. Choose **Save**\. 

**To create a new security profile for monitoring live conversations**

1. Choose **Users**, **Security profiles**\. 

1. Choose **Add new security profile**\. 

1. Expand **Analytics and optimization**, then choose **Access metrics** and **Real-time contact monitoring**\.  
![\[The Analytics and optimization section of the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-conversations-agent-permissions.png)

   **Access metrics** is needed so they can access the real\-time metrics report, which is where they choose which conversations to monitor\.

1. Expand **Contact Control Panel**, then choose **Access Contact Control Panel** and **Make outbound calls**\.   
![\[The contact control panel section of the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-conversations-agent-permissions2.png)

   These permissions are needed so they can monitor the conversation through the Contact Control Panel\.

1. Choose **Save**\. 
