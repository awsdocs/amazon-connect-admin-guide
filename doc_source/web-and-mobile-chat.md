# Concepts: Web and mobile chat capabilities in Amazon Connect<a name="web-and-mobile-chat"></a>

**Important**  
If you found this page because you need to contact Amazon for support, see [Amazon Customer Service](https://www.amazon.com/gp/help/customer/display.html) \(Amazon orders and deliveries\) or [AWS Support](http://aws.amazon.com/premiumsupport/) \(Amazon Web Services\)\.

Amazon Connect lets you build chatting features into your website\. It enables your customers to start chatting with contact center agents from any of your business applications, web or mobile\. Interactions are asynchronous, enabling your customers to start a chat with an agent or Amazon Lex bot, step away from it, and then resume the conversation again\. They can even switch devices and continue the chat\.

**Topics**
+ [Multiple channels, one experience](#unified-experience-chat)
+ [Getting started](#enable-chat)
+ [Example chat scenario](#example-chat-scenario)
+ [When do chats end?](#when-do-chats-end)
+ [Pricing](#web-and-mobile-chat-pricing)
+ [More information](#chat-more-info)

## Multiple channels, one experience<a name="unified-experience-chat"></a>

Agents have a single user interface to help customers using voice, chat, and tasks\. This reduces the number of tools that agents have to learn and the number of screens they have to interact with\. 

Chat activities integrate into your existing contact center flows and the automation that you built for voice\. You build your flows once and reuse them across multiple channels\. 

Metrics collection and the dashboards you built automatically benefit from the unified metrics across multiple channels\.

## Getting started<a name="enable-chat"></a>

To add chat capabilities to your Amazon Connect contact center and allow your agents to engage in chats, perform two steps:
+ Chat is enabled at the instance level when [an Amazon S3 bucket is created for storing chat transcripts](amazon-connect-instances.md#get-started-data-storage)\.
+ [Add chat to your agent's routing profile](routing-profiles.md)\.

Agents can then begin accepting chats through the Contact Control Panel\.

Amazon Connect provides several resources to help you add chat to your website\. For more information, see [Set up your customer's chat experience](enable-chat-in-app.md)\.

## Example chat scenario<a name="example-chat-scenario"></a>

A customer and agent are chatting\. The customer stops responding to the agent\. The agent asks "Are you there?" and doesn't get a reply\. The agent leaves the chat\. Now the chat is no longer associated with an agent\. Your flow determines what happens next\. 

In this scenario, the customer eventually sends another message \("Hey, I'm back"\) and the chat resumes\. Depending on the logic that you define in the flow, the chat can be assigned to the original agent, or a different agent or queue\.

Here's how you build this scenario:

1. Create a disconnect flow\. The following image shows the [Sample disconnect flow](sample-disconnect.md) in the flow designer\. This flow includes the following connected blocks: **Play prompt**, **Wait** which branches to three **Play prompts** \(for **Customer returned**, **Time expired**, and **Error**\), then **Transfer to queue** and **Disconnect**\.  
![\[The sample disconnect flow.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-disconnect-flow.png)

1.  In the disconnect flow, add a [Wait](wait.md) block\. The Wait block has two branches: 
   +  **Timeout**: Run this branch if the customer hasn't sent a message after a specified amount of time\. The total duration of the chat, including multiple **Wait** blocks, cannot exceed 25 hours\. 

      For example, for this branch you might just want to run a **Disconnect** block and end the chat\. 
   +  **Customer return**: Run this branch when the customer returns and sends a message\. With this branch, you can route the customer to the previous agent, previous queue, or set a new working queue or agent\. 

1.  In your inbound flow, add the [Set Disconnect Flow](set-disconnect-flow.md) block\. Use it to specify that when the agent or Amazon Lex bot has disconnected from the chat and only the customer remains, the set disconnect flow should run\. 

    In the following block, for example, we specified that the **Sample disconnect flow** should run\.   
![\[The Set disconnect flow block, the Select a flow dropdown menu, the sample disconnect flow option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow.png)

    For an example that uses the **Set disconnect flow** block, see the [Sample inbound flow](sample-inbound-flow.md)\. 

## When do chats end?<a name="when-do-chats-end"></a>

 By default, the duration for a chat conversation, including the time spent waiting when the customer isn't active, can't exceed 25 hours\. However, you can change this default duration and instead configure a custom chat duration\. You can configure a chat to last from a minimum of 1 hour \(60 minutes\) to up to 7 days \(10,080 minutes\)\. To configure a custom chat duration, call the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API and add the `ChatDurationInMinutes` parameter\. 

During an ongoing chat session, there's no limit to the number of times a customer can leave and rejoin an existing ongoing chat session\. To accomplish this, use the [Wait](wait.md) block\. For example, you might wait 12 hours for the customer to resume the chat before ending the chat session\. If the customer tries to resume the chat after 12 hours, in the flow you can have an Amazon Lex bot ask if they're contacting you about the same issue or a different one\. 

By specifying a wait time that's significantly shorter than the chat duration, you help ensure that customers have a good experience\. For instance, for a 25\-hour duration chat, it's possible for the customer to resume a chat after 24 hours and 58 minutes, and then be cut off after two minutes because the conversation ends at the 25\-hour limit\.

**Tip**  
If you're using Amazon Lex with chat, note that the default session timeout for an Amazon Lex session is 5 minutes\. The total duration for a session can't exceed 24 hours\. To change the session timeout, see [Setting the Session Timeout](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-session-timeoutg) in the *Amazon Lex Developer Guide*\. 

## Pricing<a name="web-and-mobile-chat-pricing"></a>

Chat is charged on a per use basis\. There are no required up\-front payments, long\-term commitments, or minimum monthly fees\. You pay per chat message, independently of the number of agents or customers using it\. Regional pricing may vary\. For more information, see [Amazon Connect pricing](http://aws.amazon.com/connect/pricing/)\. 

## More information<a name="chat-more-info"></a>

For more information about chat, see the following topics:
+  [Test voice, chat, and task experiences](chat-testing.md) 
+  [How routing works with multiple channels](about-routing.md#routing-profile-channels-works) 
+  [Create a routing profile](routing-profiles.md) 
+  [Amazon Connect Chat SDK and Sample Implementations](https://github.com/amazon-connect/amazon-connect-chat-ui-examples/) 