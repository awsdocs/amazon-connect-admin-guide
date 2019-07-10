# Monitor Live Conversations<a name="monitor-conversations"></a>

Managers can monitor live conversations between agents and customers, and review past conversations\. To set this up, you need to add the **Set call recording** block to your contact flow, assign managers the appropriate permissions, and then show them how to monitor the conversations\. 

**Important**  
The monitor feature works only when call recording is enabled on a contact flow\. For instructions on adding the **Set call recording** block to your contact flow, see [Set up Call Recording](set-up-recordings.md)\. 

## Assign Permissions to Monitor Live Conversations<a name="monitor-conversations-permissions"></a>

These permissions enable managers to monitor live conversations and access recordings of past conversations\. 

**To assign a manager permissions to monitor a live conversation**

1. Go to **Users**, **User management**, choose the manager, and then choose **Edit**\.

1. In the Security Profiles box, assign the manager to the **CallCenterManager** security profile\. This security profile also includes a setting that makes the icon to download recordings appear in the results of the Contact search page\. 

1. Assign the manager to the **Agent** security profile so they can access the contact control panel\. This is so they can monitor the conversation through the contact control panel\.

1. Choose **Save**\. 

**Or, to create a new security profile specific for this purpose**

1. Choose **Users**, **User management**, **Security profiles**\. 

1. Choose **Add new security profile**\. 

1. Expand **Metrics and Quality**, then choose **Manager monitor** and **Recorded conversations** \(choose both **Access** and **Enable download button**\)\. 

1. Expand **Contact Control Panel**, then choose **Access Contact Control Panel** and **Make outbound calls**\. 

1. Choose **Save**\. 

## Monitor Live Conversations with Customers<a name="w11aac19c21b9"></a>

1. Log in to your Amazon Connect instance with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Manager monitor** permission\.

1. Open the contact control panel \(CCP\) by choosing the phone icon in the top\-right corner of your screen\. You'll need the CCP open to connect to the call\. 

1. To choose the agent conversation you want to monitor, in Amazon Connect choose **Metrics and quality**, **Real\-time metrics**, **Agents**\.

1. Next to the names of agents in a live conversation, you'll see a headset icon\. Choose the icon to start monitoring the conversation\.

   When you're monitoring a conversation, the status in your CCP changes to **Monitoring**\.

1. To stop monitoring the conversation, in the CCP choose **End call**\.

   When the agent ends the conversation, monitoring stops automatically\.