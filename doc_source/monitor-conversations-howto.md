# Listen to live conversations or read live chats<a name="monitor-conversations-howto"></a>

Before you can listen to live conversations or read live chats, the Amazon Connect admin needs to [set up](monitor-conversations.md) the feature, and [assign you permissions](monitor-conversations-permissions.md)\. After that's done, you can do these steps\. 

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that has **Manager monitor** security profile permission\.

1. Open the Contact Control Panel \(CCP\) by choosing the phone icon in the top\-right corner of your screen\. You'll need the CCP open to connect to the conversation\. 

1. To choose the agent conversation you want to monitor, in Amazon Connect choose **Analytics and optimization**, **Real\-time metrics**, **Agents**\. The following image shows the **Real\-time metrics** page, with an arrow pointing to the **Agents** option\.  
![\[The real-time metrics page, the Agents option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/real-time-metrics-agents.png)

1. To monitor voice conversations: Next to the names of agents in a live voice conversation, there is an eye icon\. Choose the icon to start monitoring the conversation\. The following image shows the eye icon next to the **Voice** channel\.  
![\[The real-time metrics page, the Channels column, the voice channel.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/monitor-call-icon.png)

   When you're monitoring a conversation, the status in your CCP changes to **Monitoring**\.

1. To monitor chat conversations: For each agent you'll see the number of live chat conversations they're in\. Click on the number\. Then choose the conversation you want to start monitoring\. 

   When you're monitoring a conversation, the status in your CCP changes to **Monitoring**\.

1. To stop monitoring the conversation, in the CCP choose **End call** or **End chat**\.

   When the agent ends the conversation, monitoring stops automatically\.