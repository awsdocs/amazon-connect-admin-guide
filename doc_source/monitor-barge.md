# Barge live conversations<a name="monitor-barge"></a>

Supervisors and managers can barge into live conversations between agents and customers\. To set this up, you need to turn on the **Enhanced monitoring** capability in the Amazon Connect console, provide managers with the appropriate permissions, and show them how to barge into conversations\.

**Looking for how many people can barge the same conversation at one time? ** See [Amazon Connect feature specifications](feature-limits.md)\.

There is no limit to the number of conversations that you can barge in an instance\.

The barge feature is included in Amazon Connect voice service fees\. For pricing, see the [Amazon Connect Pricing](http://aws.amazon.com/connect/pricing/) page\.

## Set up barge for voice<a name="monitor-barge-set-up"></a>

in Amazon Connect console, select **Enable Multi\-Party Calls and Enhanced Monitoring**\. This option enables access to multi\-party calling, detailed contact records, silent monitoring, and barge capabilities\.

The following image shows the **Enable Multi\-Party Calls and Enhanced Monitoring** option on the **Telephony Options** page\.

![\[The Telephony options page, The option to enable multi-party calls and enhanced monitoring.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-barge-enhanced-monitoring-enable.png)

**Note**  
If multi\-party calling is already enabled, to also you enable enhanced monitoring you will need to use the *UpdateInstanceAttribute* API with the `ENHANCED_CONTACT_MONITORING` attribute for the first time\. Or, you can turn the feature OFF and then back ON to update your settings\. For more information, see [ UpdateInstanceAttribute](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateInstanceAttribute.html) in the *Amazon Connect API Reference Guide*\.
Any new instances will automatically have this feature enabled\.
Before enabling **Enhanced monitoring** capabilities, ensure that you are using the latest version of the [Contact Control Panel](https://docs.aws.amazon.com/connect/latest/adminguide/upgrade-to-latest-ccp.html) \(CCP\) or [Agent workspace](https://docs.aws.amazon.com/connect/latest/adminguide/agent-user-guide.html)\. If you are using [StreamsJS](https://github.com/amazon-connect/amazon-connect-streams) to customize or embed the CCP, upgrade to version 2\.4\.2 or later\.
For instances that do not have a service\-linked role, you must create one in order to enable the feature\. For more information on how to enable service\-linked roles, see [Use service\-linked roles for Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/connect-slr.html)\.

## Set up barge for voice<a name="monitor-barge-permissions"></a>

For managers to barge live conversations, you assign them the **CallCenterManager** and **Agent** security profiles\. To allow specific users to barge live conversations, you should create a security profile specific for this purpose\.

**To assign a manager permissions to barge a live conversation**

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\. Use an **Admin** account, or an account assigned to a security profile that has permissions to assign security profile permissions\.

1. On the navigation menu, choose **Users**, **User management**\. Choose the manager, and then choose **Edit**\.

1. In the *Security Profiles* box, assign the manager to the **CallCenterManager** security profile\.

1. Assign the manager to the **Agent** security profile so they can access the Contact Control Panel \(CCP\), and use it to barge into the conversation\.

1. Choose **Save**\.

**To create a new security profile for monitoring live conversations**

1. Choose **Users**, **Security profiles**\.

1. Choose **Add new security profile**\.

1. Expand **Analytics** and choose **Real\-time contact barge\-in**, as shown in the following image\.  
![\[The Real-time contact barge-in permission on the security profile page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-barge-security-profile-permissions.png)
**Note**  
For a manager to use the barge feature, both **Real\-time contact monitoring** and **Real\-time contact barge** need to enabled\.
**Access metrics** is needed so you can access real\-time metrics reports, which is where you choose which conversation you would like to monitor\.

1. Choose **Save**\.

## Barge live calls with contacts<a name="monitor-barge-how-to-use"></a>

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.\. Use an account that is assigned the **CallCenterManager** security profile or a user that has been given Real time contact monitor and barge permissions\.

1. On the navigation menu, choose **Analytics and optimization**, **Real\-time metrics**, **Agents**\.

1. Choose the eye icon that appears next to the **Voice** channel of the agent that you want to monitor, as shown in the following image\. You can barge into a conversation that you had been monitoring already\.   
![\[The Real-time metrics page, the eye icon next to a Voice channel.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-barge-voice-channel.png)

1. This opens the Contact Control Panel \(CCP\), as shown in the following image\. You can enable barge, and move between the **Monitor** and **Barge** states\.  
![\[The CCP, the Monitor and Barge toggles.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-barge-voice-channel-ccp.png)