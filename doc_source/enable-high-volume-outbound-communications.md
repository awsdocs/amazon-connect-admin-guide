# Enable High\-Volume Outbound Communications<a name="enable-high-volume-outbound-communications"></a>


|  | 
| --- |
| High\-Volume Outbound Communications is in preview release for Amazon Connect and is subject to change\. | 

Contact centers send outbound communications to customers for a variety of reasons, such as appointment reminders, telemarketing, subscription renewals, and debt collection\. By using Amazon Pinpoint Journeys and Amazon Connect, you can create high\-volume outbound campaigns for voice, SMS, and email\.  

This topic describes how to create a high\-volume outbound campaign using Amazon Connect and Amazon Pinpoint through the user interface\.  

## Before you begin<a name="campaign-prereq"></a>

There are a few things that you need in place before you create a high\-volume outbound campaign:
+ Make sure your instance is [enabled for outbound calling](enable-outbound-calls.md)\. 
+ Create a dedicated outbound communications queue to handle any contacts that will be routed to agents as a result of the campaign\.
+ Assign the queue to the agent's routing profile\.
+ Create and publish a contact flow that includes a [Check call progress](check-call-progress.md) block\. This block enables you to branch based on whether a person answered the phone, for example, or a voicemail was detected\.

## Create a high\-volume outbound campaign<a name="how-to-create-campaigns"></a>

1. In the navigation pane, choose **High volume outbound communication**, and then choose **Create campaign**\.

1. In the **Campaign details** section, specify the name\. 

1. In the **Outbound configuration** section, select the published contact flow you created for outbound communications \(a contact flow that includes a [Check call progress](check-call-progress.md) block\)\.

1. Select a queue to associate with this campaign\. When customers are routed to an agent, they will come from this queue\.

   This queue should be dedicated to outbound campaigns\. You can have multiple campaigns on the same queue\. We recommend that you don't use this queue for any other purpose, and that you don't transfer calls from this queue to a queue that's not related to this campaign\.

1. Choose the phone number to be used to make the outbound calls\. The outbound phone number is specified at the queue\. This is optional if you set an outbound number in the queue\.

   You must use a phone number that has been ported to your Amazon Connect instance, or claimed from Amazon Connect\.

1. Choose a dialer type\.

1. Choose a bandwidth allocation\.

1. Create the campaign ID\. Copy the campaign ID, because you'll use it in the next step\.

1. Open the Amazon Pinpoint console \([https://console\.aws\.amazon\.com/pinpoint/](https://console.aws.amazon.com/pinpoint/)\) and [Create a journey](https://docs.aws.amazon.com/pinpoint/latest/userguide/journeys-create.html), using the name of the campaign that you created in Amazon Connect\.

## Campaign status<a name="campaign-status"></a>

After a campaign is running, you can pause or stop it\. You can delete a campaign at any time\. 
+ **Created** – The campaign is created\.
+ **Running** – The campaign as running\.
+ **Paused** – The campaign is paused until it is resumed\.
+ **Stopped** – The campaign is stopped\. You can't resume a campaign that is stopped\.
+ **Failed** – An error state caused the campaign to fail\.