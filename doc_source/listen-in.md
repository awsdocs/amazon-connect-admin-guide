# Listen in to Calls<a name="listen-in"></a>

Managers can listen in on active calls as agents interact with customers\. To set this up, you need to add the **Set call recording** block to your contact flow, assign managers the appropriate permissions, and then show them how to listen in\. 

**Important**  
The listen\-in feature works only when call recording is enabled on a contact flow\. For instructions on adding the **Set call recording** block to your contact flow, see [Work with Recordings](recordings.md)\. 

## Assign Permissions to Listen to Calls<a name="manager-listen-in"></a>

These permissions enable managers to listen to active calls and access recordings of past calls\. 

**To assign the manager permissions to listen in to conversations**

1. Go to **Users**, **User management**, choose the manager, and then choose **Edit**\.

1. In the Security Profiles box, assign the manager to the **CallCenterManager** security profile\. This security profile also includes a setting that makes the icon to download recordings easily discoverable\. 

1. Also assign the manager to the **Agent** security profile so they can access the control contact panel\. 

1. Choose **Save**\. 

**Or, to create a new security profile specific for this purpose**

1. Choose **Users**, **User management**, **Security profiles**\. 

1. Choose **Add new security profile**\. 

1. Expand **Metrics and Quality**, then choose **Manager monitor** and **Recorded conversations** \(choose both **Access** and **Enable download button**\)\. 

1. Expand **Contact Control Panel**, then choose **Access Contact Control Panel** and **Make outbound calls**\)\. 

1. Choose **Save**\. 

## Listen in to Calls<a name="w13aac13c21b9"></a>

**To listen in on active agent calls**

1. Log in to your Amazon Connect instance with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Manager monitor** permission\.

1. Open the CCP by choosing the phone icon in the top\-right corner of your screen\. You'll need the CCP open to connect to the call\. 

1. To choose the agent call you want to listen in to, in Amazon Connect choose **Metrics and quality**, **Real\-time metrics**, **Agents**\.

1. Next to the names of agents on a call, you'll see a headset icon\. Choose the icon to start listening to the call\.

   When you're listening to call, the status in your CCP changes to **Monitoring**\.

1. To stop listening to the call, in the CCP choose **End call**\.

   When the agent ends the call, monitoring stops automatically\.