# Create an outbound campaign<a name="how-to-create-campaigns"></a>

Contact centers send outbound campaigns to customers for a variety of reasons, such as appointment reminders, telemarketing, subscription renewals, and debt collection\. By using Amazon Pinpoint Journeys and Amazon Connect, you can create outbound campaigns for voice, SMS, and email\.  

There are two ways you can create an outbound campaign:
+ Use Amazon Connect console and Amazon Pinpoint\. This topic provides instructions\.
+ Use the Amazon Connect Outbound Campaigns API\. For more information, see [Amazon Connect Outbound Campaigns API Reference](https://docs.aws.amazon.com/connect-outbound/latest/APIReference/Welcome.html)\. Note that you can't update the name of the outbound queue using the API\.

## How to create an outbound campaign<a name="create-campaigns"></a>

1. Log in to your contact center at https://*instance name*\.my\.connect\.aws/\.

1. On the left navigation menu, choose **High\-volume outbound communication**, and then choose **Create campaign**\.

1. In the **Campaign details** section, specify the name\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hvoc-create-campaign-name.png)

1. In the **Outbound configuration** section, select the published flow you created for outbound campaigns \(a flow that includes a [Check call progress](check-call-progress.md) block\)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hvoc-create-campaign-flow.png)

1. Select a queue to associate with this campaign\.

1. Answering machine detection is enabled by default\. If desired, you can choose to disable it\. 
**Note**  
If you disable answering machine detection, and if your flow includes the [Check call progress](check-call-progress.md) block, the contact is routed down the Error branch\.

1. Choose a phone number to be shown as caller ID when making outbound calls\. The outbound phone number is specified for a queue\.
**Important**  
You must use a phone number that has been ported to your Amazon Connect instance, or claimed from Amazon Connect\. 
Telecom regulations in certain countries dictate use of phone numbers from specific carriers for outbound calling\. For more information, see the [ Amazon Connect Telecoms Country Coverage Guide](https://d1v2gagwb6hfe1.cloudfront.net/Amazon_Connect_Telecoms_Coverage.pdf) to learn more\.
If you plan to call customers in Australia or New Zealand, see *Step 4: Create a new campaign in the Amazon Connect instance* in this blog for instructions: [ Make predictive and progressive calls using Amazon Connect high\-volume outbound communications](http://aws.amazon.com/blogs/contact-center/make-predictive-and-progressive-calls-using-amazon-connect-high-volume-outbound-communications/)\.

1. Choose a dialer type\.

1. Choose a bandwidth allocation\.

1. Open the Amazon Pinpoint console \([https://console\.aws\.amazon\.com/pinpoint/](https://console.aws.amazon.com/pinpoint/)\) and [Create a journey](https://docs.aws.amazon.com/pinpoint/latest/userguide/journeys-create.html), using the name of the campaign that you created in Amazon Connect\.

1. Associate this campaign to a customer journey on Amazon Pinpoint to start making high\-volume outbound calls\.

## Campaign state<a name="campaign-state"></a>

After a campaign is running, you can pause or stop it\. You can also delete a campaign at any time\. 

Following is a description of each campaign state:
+ **Created** – The campaign is created\.
+ **Running** – The campaign as running\.
+ **Paused** – The campaign is paused until it is resumed\.
+ **Stopped** – The campaign is stopped\. You can't resume a campaign that is stopped\.
+ **Failed** – An error state caused the campaign to fail\.