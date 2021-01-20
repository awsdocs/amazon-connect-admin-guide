# Enable Apple Business Chat<a name="apple-business-chat"></a>


|  | 
| --- |
| Apple Business Chat is in preview release for Amazon Connect and is subject to change\. | 

You can use Amazon Connect with Apple Business Chat to provide customer support to Apple device users directly in the Messages app\. 

This topic explains how to use Amazon Connect with Apple Business Chat\.

## Getting started<a name="getting-started-apple-business-chat"></a>

### Step 1: Register with Apple<a name="register-with-apple"></a>

Integrate Apple Business Chat with Amazon Connect by first registering with Apple as a brand\. When you do, you'll get a unique Apple Business Chat ID, and you can then link your Apple Business Chat account to Amazon Connect\. 

1. Go to the [Apple Business Chat](https://register.apple.com/business-chat) page and choose **Get Started as a brand**\.

1. Create an Apple ID for your business, if you don't already have one\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-create-apple-id.png)

   An Apple ID is typically for the personal use of Apple services, such as storing personal content in iCloud and downloading apps from the App Store\. If you have a personal Apple ID, we recommend that you create a separate one using your organization’s email address to administer Business Chat\. A separate administrative Apple ID lets you distinguish Business Chat communications from personal Apple communications\.

1. Register a profile for the a new Business Chat account by accepting **Apple’s Terms of Service** and providing business details such as a logo and support hours\.

1. Select Amazon Connect as your Messaging Service Provider\. You can do this by selecting Amazon Connect from the drop\-down or by entering the following URL:
   + https://messagingintegrations\.connect\.amazonaws\.com/applebusinesschat

After you submit your application to Apple, you’ll see the status of your application at the top of your Business Chat Account page\.

For more information about registering with Apple, see the following articles on Apple's website: [Getting Started with Business Chat](https://register.apple.com/resources/business-chat/BC-GettingStarted.pdf) and [Business Chat Policies and Best Practices](https://register.apple.com/resources/business-chat/BC-Policies_and_Best_Practices.pdf)\. 

### Step 2: Link your Apple Business Chat ID to Amazon Connect<a name="link-apple-business-chat"></a>

After you’ve been approved by Apple for Business Chat, you will be issued an Apple Business Chat ID\. 

**Note**  
Your Apple Business Chat ID is a randomized string of numbers and letters\. It is not the same as your Apple ID\. 

In this step, link your Apple Business Chat ID with your Amazon Connect instance\.

1. To find your Apple Business Chat ID, on the Apple website, go to your **Business Chat Account** page\. Scroll to the **Messaging Service Provider** section\.

1. Choose **Test your Messaging Service Provider connection**\. 

1. You will be directed to [this page](https://pages.awscloud.com/Amazon-Connect-Chat-Preview.html) \(https://pages\.awscloud\.com/Amazon\-Connect\-Chat\-Preview\.html\) where you can sign up for preview access to the Amazon Connect/Apple Business Chat integration\. 

1. To complete the integration, provide Amazon Connect with the following information:
   + Apple Business Chat ID
   + Amazon Connect instance ID: This is the identifier for instance you want to link to your Apple business account\. For help locating your instance ID, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.
   + Contact flow ID: this is the identifier for the contact flow you want to use for inbound chats\. For help locating your contact flow ID, see [Find the contact flow ID](#find-contact-flow-id)\.

   If you need help completing the Amazon Connect side of the integration, contact [AWS Support](get-admin-support.md)\.

#### Find the contact flow ID<a name="find-contact-flow-id"></a>

Amazon Connect contact flow ID is the contact flow you want to use for inbound Apple Business Chat messages\. Contact flows define the experiences for your customers when they begin a new chat\. 

Use the following steps to find your contact flow ID: 

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to view contact flows\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Select the contact flow you want to use\.

1. In the contact flow designer, expand **Show additional flow information**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-find-contactflow-id.png)

1. Under the ARN \(Amazon Resource Number\), copy everything after contact\-flow/\. For example, in the following image, you would copy the underlined part\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-find-contactflow-id-copy.png)

## Add Apple Business Chat features<a name="add-apple-business-chat-features"></a>

### Call Deflection with Apple’s Chat Suggest<a name="call-deflection"></a>

With [Chat Suggest](https://register.apple.com/resources/business-chat/BC-ChatSuggestGuide.pdf) you can allow users to choose between voice and messaging when tapping on your business phone number in Safari, Maps, Siri, or Search\. 

To enable Chat Suggest, send an email to the Apple Business Chat Team at [registry@apple\.com](registry@apple.com) with the following information and Apple can set up the channel for you: 
+ Provide all of your primary phone numbers, including high call volume phone numbers\.
+ Provide phone contact hours to set customer expectations for your after\-hours message\.
+ Provide intent, group, and body parameters to associate with each phone number\.
+ Provide an estimate of how many customers your agents can support per day\. This can be increased or decreased depending on operational capacity\.

To learn more about enabling Chat Suggest, see [Apple’s Chat Suggest FAQs](https://register.apple.com/resources/business-chat/faq/business-chat-suggest-faqs.html)\. 

### Embed Apple Business Chat buttons<a name="embed-apple-business-chat-buttons"></a>

To embed Apple Business Chat buttons on your website or mobile app, do the following:

1. Add Apple’s Business Chat JS \(JavaScript\) library to your webpage headers\.

1. Add a `div` container to house the button\.

1. Customize the banner, fallback support, and button color to meet your brand’s needs\.

The Business Chat button must contain the following, at minimum:
+ A class attribute to specify the type of container: banner, phone, or message\. For more information, see [Business Chat Button Class and Data](https://developer.apple.com/documentation/businesschat/adding_a_business_chat_button_to_your_website#3021382)\. 
+ A data\-apple\-business\-id attribute with the business ID you received when you registered your company with Business Chat\.

For information about how you can enable these buttons, see Apple’s documentation for [Adding a Business Chat Button to Your Website](https://developer.apple.com/documentation/businesschat/adding_a_business_chat_button_to_your_website#overview)\. 

### Add list pickers and time pickers<a name="list-picker"></a>

A list picker prompts your customer to select an item, such as a product or the reason for their inquiry\. A time picker prompts your customer to choose an available time slot, such as to schedule an appointment\. 

For information about how to set up list pickers and time pickers, see [Add interactive messages to chat](interactive-messages.md)\. 

## Update your contact flows<a name="apple-business-chat-flows"></a>

The contact attributes enable you to store temporary information about the contact so you can use it in the contact flow\. For example, if you have different lines of business using Apple Business Chat, you can branch to different contact flows based on the AppleBusinessChatGroup contact attribute\. Or, if you want to route Apple Business Chat messages differently from other chat messages, you can branch based on MessagingPlatform\. 

For more information about contact attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\. 

Use the following contact attributes to route Apple Business Chat customers\. 


| Attribute | Description | Type | JSON | 
| --- | --- | --- | --- | 
|  MessagingPlatform  |  The messaging platform from where the customer request originated\.  Exact value: **AppleBusinessChat**  | User\-defined | $\.Attributes\.MessagingPlatform | 
|  AppleBusinessChatCustomerId  |  The customer’s opaque ID provided by Apple\. This remains constant for customer's AppleID and a business\. You can use this to identify if the message is from a new customer or a returning customer\.  | User\-defined | $\.Attributes\.AppleBusinessChatCustomerId | 
|  AppleBusinessChatIntent  |  You can define the intent or purpose of the chat\. This parameter is included in a URL that initiates a chat session in Messages when a customer chooses the **Business Chat** button\.  | User\-defined | $\.Attributes\.AppleBusinessChatIntent | 
|  AppleBusinessChatGroup  |  You define the group which designates the department or individuals best qualified to handle the customer’s particular question or problem\. This parameter is included in a URL that initiates a chat session in Messages when a customer chooses the **Business Chat** button\.   | User\-defined | $\.Attributes\.AppleBusinessChatGroup | 
|  AppleBusinessChatLocale  |  Defines the user's language and AWS Region preferences that they want to see in their user interface\. It consists of a language identifier \(ISO 639\-1\) and a Region identifier \(ISO 3166\)\. For example, **en\_US**\.   | User\-defined | $\.Attributes\.AppleBusinessChatLocale | 