# Make a call while on a chat<a name="call-and-chat"></a>

Let's say you're chatting with a contact and you want to consult with someone else\. While you're on a chat, you can use the updated CCP to make outbound calls using the number pad and [external quick connects](quick-connects.md#external-quick-connect-type)\. 

Note the following limitations:
+ You can't access agent quick connects while you're on a chat\.
+ Agents can't receive calls while on a chat\.

**To make an external call while you're on a chat**

1. In the CCP, choose the phone tab\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/training-guide-choose-phone-while-on-chat.png)

1. Choose **Number pad**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/training-guide-choose-numberpad-while-on-chat.png)

1. Enter the external number you want to call, and then choose **Call**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/training-guide-dial-call-while-on-chat.png)

1. You'll be connected to the call at the same time the chat is still ongoing, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/training-guide-connected-call-while-on-chat.png)

1. To go to the chat conversation while you're on the phone, choose the chat tab\. 

1. To end the phone conversation, choose the phone tab, choose **End call**, and then choose **Clear contact**\. You're still connected to the chat conversation\.

## Can't make outbound call to another agent<a name="call-and-chat-troubleshooting1"></a>

If you're on a chat and having trouble making an outbound call to another agent, that agent may be handling a chat conversation\. They can't receive a call while on a chat\. 

## Can't see external quick connects in the CCP<a name="call-and-chat-troubleshooting2"></a>

 [Agent quick connects](quick-connects.md#agent-quick-connect-type) are not visible in the CCP while you're on a chat\.

If you can't see [external quick connects](quick-connects.md#external-quick-connect-type) in your CCP, however, check that the external quick connect has been added to your queue as described in [Step 2: Enable agents to see quick connects](quick-connects.md#step2-enable-agents-to-see-quick-connects)\.

## Enable agent quick connects for calls during a chat<a name="call-and-chat-enable-agent-quick-connects"></a>

To enable agents to consult over the phone with each other while they are on chats, your Amazon Connect administrator needs to set up a direct dial number \(DID\) that routes to the agent\. This configuration incurs additional costs\. 