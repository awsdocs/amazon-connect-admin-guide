# Agent training guide for the Amazon Connect CCP<a name="agent-user-guide"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to interact with customer contacts\. It's how they receive calls, chat with contacts, transfer them to other agents, put them on hold, and perform other key tasks\.

The URL to launch the CCP is:
+ **https://*name of your instance*\.awsapps\.com/connect/ccp\-v2/**

Where *name of your instance* is provided by your IT department or whoever set up Amazon Connect for your business\.

Large businesses often choose to customize their CCP\. For example, they might want to integrate it with a CRM\. However, this section describes how CCP works before it is customized\.

We recently released an updated CCP\. It provides a single interface for agents to manage both voice and chat contacts\. Even if your business is currently taking only voice contacts, we recommend using the updated CCP\.

The following image shows the CCP\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-intro.png)

**Topics**
+ [Training video](ccp-video-training.md)
+ [Agent training cheat sheet](ccp-cheat-sheet.md)
+ [Launch the CCP](launch-CCP.md)
+ [Log in and log out of the CCP](ccp-login.md)
+ [Set your status to available](set-status-available.md)
+ [Chat with contacts](work-with-chats.md)
+ [Transfer chats to another queue](transfer-chats.md)
+ [Set your status to Pending](#set-status-to-pending)
+ [Make a call while on a chat](call-and-chat.md)
+ [Accept incoming calls](work-with-calls.md)
+ [Transfer calls](transfers.md)
+ [Make outbound calls](make-outbound-calls.md)

## Set your status to Pending<a name="set-status-to-pending"></a>

When an agent is ready to handle calls or chats, they need to set their status in the CCP to **Available**\. This tells Amazon Connect they are ready to handle contacts\.

Amazon Connect uses information in the agent's [routing profile](routing-profiles.md) to determine which contacts to route to them\.