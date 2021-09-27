# Add Apple Business Chat features<a name="add-apple-business-chat-features"></a>

## Deflect calls with Apple’s Chat Suggest<a name="call-deflection"></a>

With [Chat Suggest](https://register.apple.com/resources/business-chat/BC-ChatSuggestGuide.pdf) you can allow users to choose between voice and messaging when tapping on your business phone number in Safari, Maps, Siri, or Search\. 

To enable Chat Suggest, send an email to the Apple Business Chat Team at **registry@apple\.com** with the following information and Apple can set up the channel for you: 
+ Provide all of your primary phone numbers, including high call volume phone numbers\.
+ Provide phone contact hours to set customer expectations for your after\-hours message\.
+ Provide intent, group, and body parameters to associate with each phone number\.
+ Provide an estimate of how many customers your agents can support per day\. This can be increased or decreased depending on operational capacity\.

To learn more about enabling Chat Suggest, see [Apple’s Chat Suggest FAQs](https://register.apple.com/resources/business-chat/faq/business-chat-suggest-faqs.html)\. 

## Embed Apple Business Chat buttons<a name="embed-apple-business-chat-buttons"></a>

To embed Apple Business Chat buttons on your website or mobile app, do the following:

1. Add Apple’s Business Chat JS \(JavaScript\) library to your webpage headers\.

1. Add a `div` container to house the button\.

1. Customize the banner, fallback support, and button color to meet your brand’s needs\.

The Business Chat button must contain the following, at minimum:
+ A class attribute to specify the type of container: banner, phone, or message\. For more information, see [Business Chat Button Class and Data](https://developer.apple.com/documentation/businesschat/adding_a_business_chat_button_to_your_website#3021382)\. 
+ A data\-apple\-business\-id attribute with the business ID you received when you registered your company with Business Chat\.

For information about how you can enable these buttons, see Apple’s documentation for [Adding a Business Chat Button to Your Website](https://developer.apple.com/documentation/businesschat/adding_a_business_chat_button_to_your_website#overview)\. 

## Start a chat from a URL<a name="start-chat-from-url"></a>

You can give your customers the ability to start a conversation with you from your website or an email message\.

For example, customers may start a chat using a URL that you provide\. When they click the URL, the system redirects them to Messages so they can send your business a text message\.

You decide how and where to provide the URL\. You can include it as a link in an email message, on your website, or use it as the action for a button in your app\.

Use the URL **https://bcrw\.apple\.com/urn:biz:*your\-business\-id***, replacing *your\-business\-id* with the business ID you received from Apple after registering with Business Chat\.

Following are optional query string parameters you can include in the URL:
+ `biz-intent-id`: Use to specify the intention, or purpose, of the chat\.
+ `biz-group-id`: Use to indicate the group, department, or individuals best qualified to handle the customer's specific question or problem\.
+ `body`: Use to prepopulate the message so the customer only presses **Send** to start the conversation\.

For more information, see [About Intent, Group, and Body Values](https://developer.apple.com/documentation/businesschat/bcchataction/about_intent_group_and_body_values) on the Apple Documentation website\. 

Following is an example of what the URL might look like for a customer with a credit card question question for the billing department: 
+ https://bcrw\.apple\.com/urn:biz:22222222\-dddd\-4444\-bbbb\-777777777777?biz\-intent\-id=account\_question&biz\-group\-id=billing\_department&body=Order%20additional%20credit%20card\.

## Add list pickers and time pickers<a name="add-list-pickers-time-pickers"></a>

A list picker prompts your customer to select an item, such as a product or the reason for their inquiry\. A time picker prompts your customer to choose an available time slot, such as to schedule an appointment\. 

For information about how to set up list pickers and time pickers, see [Add interactive messages to chat](interactive-messages.md)\. 

## Use rich links for URLs<a name="rich-links"></a>

Rich links show an inline preview of a URL that contains an image\. Unlike normal URLs, customers can view the image immediately in a chat without choosing a "Tap to Load Preview" message\. 

To learn more about Apple Business Chat rich links, see [Rich Links](https://developer.apple.com/design/human-interface-guidelines/business-chat/interactive-messages/rich-links/) on the Apple Developer website\.

### Requirements for using rich links in Amazon Connect<a name="rich-links-requirements"></a>

To use rich links in Amazon Connect chat messages, your URL and images must meet the following requirements:
+ Your website must use Facebook Open Graph tags\. For more information, see [A Guide to Sharing for Webmasters](https://developers.facebook.com/docs/sharing/webmasters/)\. 
+ The image accompanying the URL must be \.jpeg, \.jpg, or \.png\.
+ The website must be HTML\.

**Note**  
When you first use the rich link feature, we recommend that you send the URL in a message separate from your chat text, as shown in the following example\.  

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-rich-link.png)

## Use Apple Business Chat contact attributes in contact flows<a name="apple-business-chat-flows"></a>

Contact attributes enable you to store temporary information about the contact so you can use it in the contact flow\. 

For example, if you have different lines of business using Apple Business Chat, you can branch to different contact flows based on the **AppleBusinessChatGroup** contact attribute\. Or, if you want to route Apple Business Chat messages differently from other chat messages, you can branch based on MessagingPlatform\. 

For more information about contact attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\. 

Use the following contact attributes to route Apple Business Chat customers\. 


| Attribute | Description | Type | JSON | 
| --- | --- | --- | --- | 
|  MessagingPlatform  |  The messaging platform from where the customer request originated\.  Exact value: **AppleBusinessChat**  | User\-defined | $\.Attributes\.MessagingPlatform | 
|  AppleBusinessChatCustomerId  |  The customer’s opaque ID provided by Apple\. This remains constant for the AppleID and a business\. You can use this to identify if the message is from a new customer or a returning customer\.  | User\-defined | $\.Attributes\.AppleBusinessChatCustomerId | 
|  AppleBusinessChatIntent  |  You can define the intent or purpose of the chat\. This parameter is included in a URL that initiates a chat session in Messages when a customer chooses the **Business Chat** button\.  | User\-defined | $\.Attributes\.AppleBusinessChatIntent | 
|  AppleBusinessChatGroup  |  You define the group which designates the department or individuals best qualified to handle the customer’s particular question or problem\. This parameter is included in a URL that initiates a chat session in Messages when a customer chooses the **Business Chat** button\.   | User\-defined | $\.Attributes\.AppleBusinessChatGroup | 
|  AppleBusinessChatLocale  |  Defines the language and AWS Region preferences that the user wants to see in their user interface\. It consists of a language identifier \(ISO 639\-1\) and a Region identifier \(ISO 3166\)\. For example, **en\_US**\.   | User\-defined | $\.Attributes\.AppleBusinessChatLocale | 