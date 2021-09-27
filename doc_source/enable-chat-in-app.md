# Set up your customer's chat experience<a name="enable-chat-in-app"></a>

You can provide a chat experience to your customers by using one of the following methods: 
+ [Add a chat user interface to your website](add-chat-to-website.md)\. 
+ [Download and customize our open source example](download-chat-example.md)\. 
+ [Customize your solution using Amazon Connect APIs](integrate-with-startchatconnect-api.md)\. We recommend starting with the Amazon Connect ChatJS open source library when customizing your own chat experiences\. For more information, see the [Amazon Connect ChatJS](https://github.com/amazon-connect/amazon-connect-chatjs) repo on Github\. 

## More resources to customize the chat experience<a name="more-resource-customize-chat"></a>
+ Interactive messages provide customers with a prompt and pre\-configured display options that they can select from\. These messages are powered by Amazon Lex and configured through Amazon Lex using a Lambda\. For instructions about how to add interactive messages through Amazon Lex, see this blog: [Set up interactive messages for your Amazon Connect chatbot](https://aws.amazon.com/blogs/contact-center/easily-set-up-interactive-messages-for-your-amazon-connect-chatbot/)\.

  Amazon Connect supports the following templates: a list picker and a time picker\. For more information, see [Add interactive messages to chat](interactive-messages.md)\. 
+  [Enable Apple Business Chat](apple-business-chat.md) 
+  [Amazon Connect Service API Documentation](https://docs.aws.amazon.com/connect/latest/APIReference), especially the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API\.
+  [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html)\. 
+  [ Amazon Connect Chat SDK and Sample Implementations](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/) 
+  [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams)\. Use to integrate your existing apps with Amazon Connect\. You can embed the Contact Control Panel \(CCP\) components into your app\. 