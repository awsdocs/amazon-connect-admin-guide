# Get started with Amazon Connect<a name="amazon-connect-get-started"></a>

Use these steps to set up your contact center\.  

1. [Create an Amazon Connect instance](amazon-connect-instances.md)\. Use an instance to contain all the resources and settings related to your contact center\. You specify how you plan to manage user accounts, whether your contact center will accept incoming calls and make outbound calls, and review the location where data will be stored in your Amazon S3 bucket\. 

1. [Set up phone numbers for your contact center](contact-center-phone-number.md)\. If you're using voice, either claim a phone number that AWS provides, or port your current phone number to Amazon Connect\. If you choose to port your numbers, we suggest claiming a number so you can test Amazon Connect and build your contact center while waiting for your numbers to be ported over\. 

1. [Set up routing](connect-queues.md)\. Create your queues and routing profiles, and set your hours of operation\. In your routing profiles, specify the channels that agents should use: voice, chat, tasks, or all three\. You also specify how many chats and tasks an agent can manage at the same time\.

1. [Create Amazon Connect contact flowsCreate contact flows](connect-contact-flows.md)\. Establish a contact flow to define the customer experience with your contact center from start to finish\. A single contact flow works for voice, chat, and tasks, which makes your design more efficient\. When you build contact flows and configure the blocks, indicate how the flow should work for voice, chat, and tasks\. 

1. Add users, which are your managers and agents, and configure their settings\. Assign a routing profile to each agent, specify whether they are using a softphone or desk phone, and set how long they have for **After contact work**\. For instructions, see [Add users to Amazon Connect](user-management.md) and [Set up agents](connect-agents.md)\. 

1. If you're using chat, we provide several tools to help you enable your customer\-facing app to engage with Amazon Connect chat\. For more information, see [Set up your customer's chat experience](enable-chat-in-app.md)\. 

## Next steps<a name="w709aac10b7"></a>

There's a lot you can do to optimize your contact center\. Here are a couple of additional steps that you may find useful: 

1. [Set up recording behavior](set-up-recordings.md)\. Monitor live conversations and review past conversations\. This is a way that managers can coach agents and help them improve\. For voice conversations, set up recording in your contact flows\. For chat conversations, set up recording at the instance level\. 

   To learn how to monitor conversations, see [Monitor live conversations](monitor-conversations.md)\.

1. [Add an Amazon Lex bot](amazon-lex.md)\. Use Amazon Lex in your contact center to reduce the load on your agents\. For example, a bot can handle the initial interaction before the chat is routed to an agent, and also answer common questions for the customer\. 

## Take a free online class<a name="w709aac10b9"></a>

Check out the following free online classes:
+  [Introduction to Amazon Connect and the Contact Control Panel \(CCP\)](https://explore.skillbuilder.aws/learn/course/external/view/elearning/12303/introduction-to-amazon-connect-and-the-connect-control-panel-ccp) 
+  [Amazon Connect: Introduction to the Administrative Interface](https://explore.skillbuilder.aws/learn/course/external/view/elearning/12328/amazon-connect-introduction-to-the-administrative-interface) 
+  [Amazon Connect: Creating and Managing Amazon Connect Instances](https://explore.skillbuilder.aws/learn/course/external/view/elearning/12304/amazon-connect-creating-and-managing-amazon-connect-instances) 