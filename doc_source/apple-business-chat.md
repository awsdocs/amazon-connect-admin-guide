# Enable Apple Business Chat<a name="apple-business-chat"></a>

Your customers can engage directly with your contact center from within their Messages application on their iPhone, iPad, and Mac\. 

When you enable Apple Business Chat, your customers can find answers to their questions and request help from agents to resolve issues — all while using the familiar Messages application they use every day to chat with friends and family\. Any time customers use Search, Safari, Spotlight, Siri, or Maps to call your registered phone number, they will be provided with the option to chat with your contact center\. 

Apple Business Chat integration with Amazon Connect enables you to use the same configuration, analytics, routing, and agent UI that you already use for [Amazon Connect Chat](chat.md)\.

## Step 1: Register with Apple<a name="register-with-apple"></a>

Integrate Apple Business Chat with Amazon Connect by first registering with Apple as a brand\. When you do, you'll get a unique Apple Business Chat Account ID, and you can then link your Apple Business Chat account to Amazon Connect\. 

1. Go to the [Apple Business Chat](https://register.apple.com/business-chat) page and choose **Get Started as a brand**\.

1. Create an Apple ID for your business, if you don't already have one\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-create-apple-id.png)

   An Apple ID is typically for the personal use of Apple services, such as storing personal content in iCloud and downloading apps from the App Store\. If you have a personal Apple ID, we recommend that you create a separate one using your organization’s email address to administer Business Chat\. A separate administrative Apple ID lets you distinguish Business Chat communications from personal Apple communications\.

1. Register a profile for a new Business Chat account by accepting **Apple’s Terms of Service**\. We recommend creating a [Commercial Business Chat Account](https://register.apple.com/resources/messages/messaging-documentation/register-your-acct#create-a-commercial-business-chat-account)\. You then provide business details, such as a logo and support hours\.

1. Select Amazon Connect as your Messaging Service Provider\. You can do this by selecting Amazon Connect from the drop\-down or by entering the following URL:
   + **https://messagingintegrations\.connect\.amazonaws\.com/applebusinesschat**

After you submit your application to Apple, you’ll see the status of your application at the top of your **Business Chat Account** page\.

For more information about registering with Apple, see the following articles on Apple's website: [Getting Started with Business Chat](https://register.apple.com/resources/business-chat/BC-GettingStarted.pdf) and [Business Chat Policies and Best Practices](https://register.apple.com/resources/business-chat/BC-Policies_and_Best_Practices.pdf)\. 

## Step 2: Gather required information<a name="gather-apple-business-chat-information"></a>

Gather the following information so you have it on hand when you open a support ticket in Step 3:

1. **Apple Business Chat Account ID**: After you’ve been approved by Apple for Business Chat, you will be issued an Apple Business Chat Account ID\. For information about locating your Apple Business Chat Account ID, see [Find your Apple Business Chat Account ID](find-apple-business-chat-account-id.md)\. 
**Note**  
Your Apple Business Chat Account ID is a randomized string of numbers and letters\. It is not the same as your Apple ID\. 

1. **Apple Token**: This is a unique ID that authenticates your account\. For help locating your Apple token, see [Find your Apple token](find-apple-token-id.md)\.

1. **Amazon Connect instance ARN**: This is the identifier for the instance you want to link to your Apple business account\. For information about locating your instance ID, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.
**Note**  
Make sure you have service\-linked roles enabled for the integration\.   
If your instance was created before **October 2018**, add the `connect:*` policy on the role that is associated with your Amazon Connect instance\. For more information about service\-linked roles, see [Use service\-linked roles for Amazon Connect](connect-slr.md)\. 

1. **Amazon Connect contact flow ID**: This is the identifier for the contact flow you want to use for inbound chats\. For information about locating your contact flow ID, see [Find the contact flow ID](find-contact-flow-id.md)\.

## Step 3: Link your Apple Business Chat ID to Amazon Connect<a name="link-apple-business-chat"></a>

In this step you create an Amazon Connect support ticket to link your Apple Business Chat ID to Amazon Connect\. 

1. Create a [special AWS Support ticket](https://console.aws.amazon.com/support/home#/case/create?issueType=customer-service&serviceCode=customer-account&categoryCode=activation) to link your Apple Business Chat to Amazon Connect\.

   If prompted, login using your AWS account\.
**Tip**  
Looking for technical support? [Open an AWS Support ticket here](https://console.aws.amazon.com/support/home)\. 

1. In the **Use case description** box, copy and paste the following template: 

   ```
   Subject: Apple Business Chat Integration request
   Body:
      Apple Business Chat Account ID (required): enter your account ID
      Apple Token (required): enter your Apple token
      Amazon Connect Instance ARN (required): enter your instance ARN
      Amazon Connect Contact Flow ID (required): enter your contact flow ID
   ```

   The following image shows an example of a completed ticket:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-sample-use-case-description.png)

1. Expand **Contact options**, and then choose your **Preferred contact language**, and then choose **Web** as the contact method, if it's not selected by default\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-contact-support-options.png)

1. Choose **Submit**\.

1. AWS Support will work directly with the Amazon Connect team on your request and follow up with any additional questions\.

### Next steps<a name="enable-apple-business-chat-next-steps"></a>

After Apple Business Chat is enabled for your Amazon Connect instance, you can [ add Apple Business Chat features](add-apple-business-chat-features.md) to your messages\. For example:
+ Deflect calls with Apple's Chat Suggest\.
+ Embed Apple Business Chat buttons on your website\.
+ Add list pickers and time pickers to your messages\.
+ Use rich links for URLs\.
+ Route Apple Business Chat messages using contact attributes\.