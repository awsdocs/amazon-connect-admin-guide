# Chat with contacts<a name="work-with-chats"></a>

When you set your status in the CCP to **Available**, Amazon Connect delivers calls or chats to you, based on the settings in your [routing profile](routing-profiles.md)\. An administrator can specify that up to five chat conversations can be routed to you at the same time\. 

You can't initiate chat conversations from the CCP\.

**Note**  
IT Administrators: To enable customers and agents to send attachments, such as files, through the chat interface, see [Enable attachments to share files using chat](enable-attachments.md)\.

**Tip**  
Amazon Connect routes contacts to you for only one channel at a time\. When you're on a call, you won't be routed a chat conversation\. And when you're handling chat conversations, you won't be routed a call\.

When a chat contact arrives, here's how you are notified:

1. If you enabled notifications in your browser, you'll get a pop\-up notification at the bottom of your screen, like this:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chat-notify.png)

1. If you're on the chat tab, the page displays the name of the contact and a button for you to connect to the chat\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/incoming-chat-ccp.png)

1. If you're on the phone tab, a banner displays the name of the contact and a button for you to connect to the chat\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chat-incoming-banner.png)

1. You have 20 seconds to accept or reject a contact\. If you're on a chat, and another comes in but you don't accept it, a tab appears indicating the chat was missed\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/missed-chat-tab.png)

1. Choose **Accept chat** to connect to the contact\. 
**Note**  
Chat conversations must be accepted manually\. There's no auto\-accept for these conversations\.

1. You'll see the full transcript of what the contact has already typed\. If applicable, you'll also see what a bot or another agent has entered\. In the following image, **John** is the name of the customer, **BOT** is the Amazon Lex bot, and **Jane** is the name of the agent\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-chat-agent.png)

## What do the timers at the top of the chat tabs mean?<a name="timer-in-chat-windows"></a>

When you're in a chat conversation with a contact, you'll see two timers at the top of the chat tab\. These timers tell you: 
+ How long the contact has been connected to your contact center\. This includes the time spent with the bot, if you're using one\.
+ How long since the last text was sent\. This can be either from the customer to the agent, or from the agent to the customer\. the timer is reset with each text message\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chat-timers.png)

If you have multiple chat tabs open, an hour glass appears letting you know which ones are in an After Contact Work \(ACW\) state\. The timer indicates how long the contact has been in ACW\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chat-acw.png)

## What happens to missed chats?<a name="missed-chats"></a>

Let's say you take a break but forget to change your status in the CCP from **Available** to **Break**\. Amazon Connect tries to route a chat to you for 15 seconds\. Keep in mind that your admin can't configure this amount of time\. 

After 15 seconds, the contact is counted as [Agent non\-response](real-time-metrics-definitions.md#agent-non-response-real-time) in the real\-time metrics report and the historical metrics report\.

When you return from break and choose the chat tab, you'll see the missed contacts and how long they've been there\. Each contact occupies a slot\. This way, with all of your slots are occupied, Amazon Connect won't route any more contacts to you\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/missed-chat-name.png)

You can clear the slots so that chats are routed to you again\. For each missed contact, choose the banner, and then choose **Clear contact**\. 