# Test a Voice or Chat Experience<a name="chat-testing"></a>

To learn what the voice and chat experiences are like for your agents and customers, you can test them without doing any development\.

**To test voice**: once you claim a number you can immediately call it to hear what the experience will be like for your customers\. Amazon Connect uses the [default contact flows](contact-flow-default.md) to power your initial experience\. To test a customized contact flow, [assign a phone number](associate-phone-number.md) to it and then call that number\.

**To test chat**: Amazon Connect includes a simulated web page that shows how your customers can interact with you, and a Contact Control Panel \(CCP\) that shows the agent experience\. Here's how to test chat:

1. Go to the Amazon Connect Dashboard, and choose **Test chat**\.

   If you don't see the option to test chat, click [here](https://github.com/amazon-connect/amazon-connect-chat-ui-examples#enabling-chat-in-an-existing-amazon-connect-contact-center)\.

1. On the **Test Chat** page, choose **Test Settings**\.

1. Under **System Settings**, choose the contact flow you want to test with chat, and then click **Apply**\. By default, it runs the [Sample Inbound Flow](sample-inbound-flow.md)\.

1. In the chat window, click the icon as shown below\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-chat-icon.png)

1. Type a message similar to what one of your customers might type\. In the agent window, type a reply\.

1. To see what it's like for an agent to handle multiple chat conversations, copy the dashboard URL into another browser window, and start another chat\. The chat goes to the same instance of the CCP that you already have open\.
**Tip**  
The test environment uses the BasicQueue and Basic Routing Profile\. The Basic Routing Profile is set up for 2 chats\. If you want to test what it's like to have more than two chats, change the Basic Routing Profile to 5 chats\. For instructions, see [Create a Routing Profile](routing-profiles.md)\. 

   To learn more about what the agent experiences when managing chat conversations, see [Chat with Contacts](work-with-chats.md)\. 