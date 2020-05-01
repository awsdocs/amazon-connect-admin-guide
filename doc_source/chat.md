# Chat<a name="chat"></a>

Amazon Connect allows your customers to start a chat with an agent or Amazon Lex bot, step away from it, and then resume the conversation again\. They can even switch devices and continue the chat\. It's an asynchronous interaction\. [Learn more](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md)\.

## Example Chat Scenario<a name="example-chat-scenario"></a>

Suppose a customer and agent are chatting, but then the customer stops responding to the agent\. The agent asks "Are you there?" and doesn't get a reply\. The agent leaves the chat\. Now the chat is no longer associated with an agent; your contact flow determines what happens next\. 

In this scenario let's say the customer eventually sends another message \("Hey, I'm back"\) and the chat resumes\. Depending on the logic you define in the contact flow, the chat can be assigned to the original agent, or a different agent/queue\.

Here's how you build this scenario:

1. Create a disconnect flow\. The following image shows the [Sample Disconnect Flow](sample-disconnect.md)\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-disconnect-flow.png)

1. In the disconnect flow, add a [Wait](wait.md) block\. The Wait block has two branches:
   + **Timeout**: Run this branch if the customer hasn't sent a message after a specified amount of time\. The total duration of the chat, including multiple **Wait** blocks, cannot exceed 25 hours\.

     For example, for this branch you might just want to run a **Disconnect** block and end the chat\. 
   + **Customer return**: Run this branch when the customer returns and sends a message\. With this branch you can route the customer to the previous agent, previous queue, or set a new working queue/agent\.

1. In your inbound contact flow, add the [Set Disconnect Flow](set-disconnect-flow.md) block\. Use it to specify that when the agent or Amazon Lex bot has disconnected from the chat and only the customer remains, the set disconnect flow should run\.

   In the following block, for example, we specified that the **Sample disconnect flow** should run\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow.png)

   For an example that uses the **Set disconnect flow** block, see the [Sample Inbound Flow](sample-inbound-flow.md)\. 

## When Do Chats End?<a name="when-do-chats-end"></a>

The total duration for a chat conversation, including the time spent waiting when the customer isn't active, can't exceed 25 hours\. After that the chat conversation ends\. 

During the 25 hours, there's no limit to the number of times a customer can stop and resume chat\.

To specify wait time a shorter than 25 hours, use the [Wait](wait.md) block\. For example, you might wait 12 hours for the customer to resume the chat\. If the customer tries to resume the chat after 12 hours, in the flow you can have an Amazon Lex bot ask if they're contacting you about the same issue or a different one\.

By specifying a shorter wait time, you'll ensure customers have a good experience\. Otherwise, it's possible for the customer to resume a chat after 24 hours and 58 minutes, and then be cut off after two minutes because the conversation ends automatically at the 25 hour limit\.

**Tip**  
If you're using Amazon Lex with chat, note that the default session timeout for an Amazon Lex session is 5 minutes\. The total duration for a session can't exceed 24 hours\. To change the session timeout, see [Setting the Session Timeout](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-session-timeoutg) in the *Amazon Lex Developer Guide*\. 

## Enabling Your App for Chat<a name="enable-chat-in-app"></a>

With only a few steps, you can enable your app to engage with Amazon Connect chat\. Use the [sample implementation](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/asyncCustomerChatUX) on GitHub to help you get started\. Here's how it works:
+ It spins up an Amazon API Gateway endpoint that triggers a Lambda function\.
+ The Lambda function invokes the Amazon Connect Service [StartChatConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API and returns the result from that call\. 
+ After you spin up the AWS CloudFormation stack you can call this API from your app, import the pre\-built chat widget, pass the response to the widget, and start chatting\. 

In addition, see these resources to customize the chat experience: 
+ [Amazon Connect Service API Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html), especially the [StartChatConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API\. 
+  [Amazon Connect Participant Service API](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html)\. 
+  [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams)\. Use to integrate your existing apps with Amazon Connect\. You can embed the Contact Control Panel \(CCP\) components into your app\. 
+ [Amazon Connect Chat SDK and Sample Implementations](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/) 

## Chat Initiation Method: API<a name="chat-initiation-method"></a>

The [StartChatConnect ](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API is used to start the chat\.

When you start exploring the chat experience for the first time, you'll notice that chats aren't counted in the **Contacts Incoming** metric in your historical metrics report\. This is because the initiation method for the chat in the Contact Trace Record \(CTR\) is **API**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-api.png)

After a chat is transferred to an agent, the **Contacts Incoming** metric is incremented\. The CTR for the transfer no longer increments the API, but it does increment **Contacts Incoming**\. 

## Chat Encryption<a name="chat-encryption"></a>

Chat messages are encrypted end\-to\-end\. We use a service\-owned key that is unique to the instance for encrypting and saving messages\. 

A customer\-provided encryption key is used to encrypt transcripts that are stored in Amazon S3\. 

Chat encryption allows for use cases where security is critical, such as authenticated secure chat in mobile banking applications\.

## More Information<a name="chat-more-info"></a>

To learn more about chat, check out the following topics:
+ [Test a Voice or Chat Experience](chat-testing.md) 
+ [How Routing Works with Multiple Channels](about-routing.md#routing-profile-channels-works) 
+ [Create a Routing Profile](routing-profiles.md) 
+ [Amazon Connect Chat SDK and Sample Implementations](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/) 