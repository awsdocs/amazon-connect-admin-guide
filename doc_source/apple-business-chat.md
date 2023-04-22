# Enable Apple Messages for Business<a name="apple-business-chat"></a>

Your customers can engage directly with your contact center from within their Messages application on their iPhone, iPad, and Mac\. 

When you enable Apple Messages for Business, your customers can find answers to their questions and request help from agents to resolve issues — all while using the familiar Messages application they use every day to chat with friends and family\. Any time customers use Search, Safari, Spotlight, Siri, or Maps to call your registered phone number, they will be provided with the option to chat with your contact center\. 

Apple Messages for Business integration with Amazon Connect enables you to use the same configuration, analytics, routing, and agent UI that you already use for [Amazon Connect Chat](web-and-mobile-chat.md)\.

## Step 1: Register with Apple<a name="register-with-apple"></a>

Integrate Apple Messages for Business with Amazon Connect by first registering with Apple as a brand\. When you do, you'll get a unique Apple Messages for Business Account ID, and you can then link your Apple Messages for Business account to Amazon Connect\. 

1. Go to the [Apple Messages for Business](https://register.apple.com/business-chat) page\. In the box that says **As a business, I want to connect with my customers in the Messages app**, choose **Get Started**\.

1. Create an Apple ID for your business, if you don't already have one\.

   An Apple ID is typically for the personal use of Apple services, such as storing personal content in iCloud and downloading apps from the App Store\. If you have a personal Apple ID, we recommend that you create a separate one using your organization’s email address to administer Messages for Business\. A separate administrative Apple ID lets you distinguish Messages for Business communications from personal Apple communications\.

1. Register a profile for a new Messages for Business account by accepting **Apple’s Terms of Service**\. We recommend creating a [Commercial Messages for Business Account](https://register.apple.com/resources/messages/messaging-documentation/register-your-acct#create-a-commercial-business-chat-account)\. You then provide business details, such as a logo and support hours\.

1. Select Amazon Connect as your Messaging Service Provider\. You can do this by selecting Amazon Connect from the drop\-down or by entering the following URL:
   + **https://messagingintegrations\.connect\.amazonaws\.com/applebusinesschat**

After you submit your application to Apple, you’ll see the status of your application at the top of your **Messages for Business Account** page\.

For more information about registering with Apple, see the following articles on Apple's website: [Getting Started with Messages for Business](https://register.apple.com/resources/business-chat/BC-GettingStarted.pdf) and [Messages for Business Policies and Best Practices](https://register.apple.com/resources/business-chat/BC-Policies_and_Best_Practices.pdf)\. 

## Step 2: Gather required information<a name="gather-apple-business-chat-information"></a>

Gather the following information so you have it on hand when you open a support ticket in Step 3:

1. **Apple Messages for Business Account ID**: After you’ve been approved by Apple Messages for Business, you will be issued an Apple Messages for Business Account ID\. For information about locating your Apple Messages for Business Account ID, see [Find your Apple Messages for Business Account ID](find-apple-business-chat-account-id.md)\. 
**Note**  
Your Apple Messages for Business Account ID is a randomized string of numbers and letters\. It is not the same as your Apple ID\. 

1. **Apple Token**: This is a unique ID that authenticates your account\. For help locating your Apple token, see [Find your Apple token](find-apple-token-id.md)\.

1. **Amazon Connect instance ARN**: This is the identifier for the instance you want to link to your Apple business account\. For information about locating your instance ID, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.
**Note**  
Make sure you have service\-linked roles enabled for the integration\.   
If your instance was created before **October 2018**, add the `connect:*` policy on the role that is associated with your Amazon Connect instance\. For more information about service\-linked roles, see [Use service\-linked roles for Amazon Connect](connect-slr.md)\. 

1. **Amazon Connect flow ID**: This is the identifier for the flow you want to use for inbound chats\. For information about locating your flow ID, see [Find the flow ID](find-contact-flow-id.md)\.

## Step 3: Link your Apple Messages for Business ID to Amazon Connect<a name="link-apple-business-chat"></a>

In this step you create an Amazon Connect support ticket to link your Apple Messages for Business ID to Amazon Connect\. 

1. Create a [special AWS Support ticket](https://console.aws.amazon.com/support/home#/case/create?issueType=customer-service&serviceCode=customer-account&categoryCode=activation) to link your Apple Messages for Business to Amazon Connect\.

   If prompted, login using your AWS account\. 
**Tip**  
Looking for technical support? [Open an AWS Support ticket here](https://console.aws.amazon.com/support/home)\. 

1. Choose **Account and billing**\.

1. Use the dropdown box to choose **Account**\. For **Category** choose **Activation**, and then choose **Next step: Additional information**\.

1. For **Subject** enter **Apple Messages for Business Integration request**\.

1. In the **Description** box, copy and paste the following template: 

   ```
   Subject: Apple Messages for Business Integration request
      Body:
   
      Apple Messages for Business Account ID (required): enter your account ID
      Apple Token (required): enter your Apple token
      Amazon Connect Instance ARN (required): enter your instance ARN
      Amazon Connect Flow ID (required): enter your flow ID
   ```

   The following image shows an example of a completed ticket:  
![\[An example completed ticket.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-sample-use-case-description.png)

1. Choose **Next step**\.

1. Choose **Contact us**, choose your **Preferred contact language**, and then choose **Web** as the contact method, if it's not selected by default\.  
![\[The contact methods.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-contact-support-options.png)

1. Choose **Submit**\.

1. AWS Support will work directly with the Amazon Connect team on your request and follow up with any additional questions\.

### Next steps<a name="enable-apple-business-chat-next-steps"></a>

After Apple Messages for Business is enabled for your Amazon Connect instance, you can [ add Apple Messages for Business features](add-apple-business-chat-features.md) to your messages\. For example:
+ Deflect calls with Apple's Message Suggest\.
+ Embed Apple Messages for Business buttons on your website\.
+ Add list pickers and time pickers to your messages\.
+ Use rich links for URLs\.
+ Route Apple Messages for Business messages using contact attributes\.