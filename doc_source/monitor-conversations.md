# Monitor live conversations<a name="monitor-conversations"></a>

Managers and agents in training can monitor live conversations between agents and customers\. To set this up, you need to add the **Set recording behavior** block to your voice/chat contact flow, assign managers and trainees the appropriate permissions, and then show them how to monitor the conversations\.

**Looking for how many people can monitor the same conversation at one time?** See [Feature specifications](amazon-connect-service-limits.md#feature-limits)\.

## Set up live monitoring for voice and/or chat<a name="monitor-conversations-set-up"></a>

1. Add the [Set recording and analytics behavior](set-recording-behavior.md) block to your contact flow\. Do this to monitor calls, chats, or both\. 

   To enable monitoring of voice and/or chat conversations, in the block's properties choose **Agent and Customer**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior.png)

   For more information, see [Set up recording behavior](set-up-recordings.md)\. 

1. Choose whether to record the conversations you monitor\. 

   Although you need to add the **Set recording behavior** block to your contact flow, you don't need to record voice and/or chat conversations for monitoring to work\. By default when you set up your instance, [Amazon S3 buckets are created](amazon-connect-instances.md#get-started-data-storage) to store call recordings and chat transcripts\. The existence of these buckets enables call recording and chat transcripts at the instance level\. To not record the calls or chats you're monitoring, remove the Amazon S3 buckets\. For instructions, see [Update instance settings](update-instance-settings.md)\.

## Assign permissions to monitor live conversations<a name="monitor-conversations-permissions"></a>

For managers to monitor live conversations, you assign them the **CallCenterManager** and **Agent** security profiles\. To allow agent trainees to monitor live conversations, you may want to create a security profile specific for this purpose\.

**To assign a manager permissions to monitor a live conversation**

1. Go to **Users**, **User management**, choose the manager, and then choose **Edit**\.

1. In the Security Profiles box, assign the manager to the **CallCenterManager** security profile\. This security profile also includes a setting that makes the icon to download recordings appear in the results of the **Contact search** page\. 

1. Assign the manager to the **Agent** security profile so they can access the Contact Control Panel \(CCP\), and use it to monitor the conversation\.

1. Choose **Save**\. 

**To create a new security profile for monitoring live conversations**

1. Choose **Users**, **Security profiles**\. 

1. Choose **Add new security profile**\. 

1. Expand **Metrics and Quality**, then choose **Access metrics** and **Manager monitor**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-conversations-agent-permissions.png)

   **Access metrics** is needed so they can access the real\-time metrics report, which is where they choose which conversations to monitor\.

1. Expand **Contact Control Panel**, then choose **Access Contact Control Panel** and **Make outbound calls**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-conversations-agent-permissions2.png)

   These permissions are needed so they can monitor the conversation through the Contact Control Panel\.

1. Choose **Save**\. 

## Monitor live conversations with contacts<a name="w463aac49b7c11"></a>

**Tip**  
Call barge\-in is not currently supported\. That is, if you're listening to a conversation, your microphone stays muted\.

1. Check that the [Set recording and analytics behavior](set-recording-behavior.md) block is in the contact flow you want to monitor\. It has to be there whether you're monitoring calls or chats\. In the block's Properties, choose **Agent and Customer**\.

1. Log in to your Amazon Connect instance with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Manager monitor** permission\.

1. Open the Contact Control Panel \(CCP\) by choosing the phone icon in the top\-right corner of your screen\. You'll need the CCP open to connect to the conversation\. 

1. To choose the agent conversation you want to monitor, in Amazon Connect choose **Metrics and quality**, **Real\-time metrics**, **Agents**\.

1. To monitor voice conversations: Next to the names of agents in a live voice conversation, you'll see a headset icon\. Choose the icon to start monitoring the conversation\.

   When you're monitoring a conversation, the status in your CCP changes to **Monitoring**\.

1. To monitor chat conversations: For each agent you'll see the number of live chat conversations they're in\. Click on the number\. Then choose the conversation you want to start monitoring\. 

   When you're monitoring a conversation, the status in your CCP changes to **Monitoring**\.

1. To stop monitoring the conversation, in the CCP choose **End call** or **End chat**\.

   When the agent ends the conversation, monitoring stops automatically\.