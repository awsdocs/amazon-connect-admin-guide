# Download and customize our open source example<a name="download-chat-example"></a>

You can further customize the chat experience customers use to interact with agents\. Use the [ Amazon Connect open source library](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/asyncCustomerChatUX) on GitHub\. It's a platform to help you get started quickly\. Here's how it works:
+ The GitHub repository links to a CloudFormation template, which starts the Amazon API Gateway endpoint that initiates a Lambda function\. You can use this template as an example\.
+ After you create the AWS CloudFormation stack, you can call this API from your app, import the pre\-built chat widget, pass the response to the widget, and start chatting\. 

For more information about customizing the chat experience, see: 
+ [Amazon Connect Service API Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html), especially the [StartChatConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API\. 
+  [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html)\. 
+  [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams)\. Use to integrate your existing apps with Amazon Connect\. You can embed the Contact Control Panel \(CCP\) components into your app\. 
+ [Amazon Connect Chat SDK and Sample Implementations](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/) 