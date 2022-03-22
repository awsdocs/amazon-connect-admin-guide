# Test voice, chat, and task experiences<a name="chat-testing"></a>

To learn what the voice, chat, and task experiences are like for your agents and customers, you can test them without doing any development\.

## Test voice<a name="test-voice"></a>

After you claim a number you can immediately call it to hear what the experience will be like for your customers\. Amazon Connect uses the [default contact flows](contact-flow-default.md) to power your initial experience\. 

To test a customized contact flow, [assign a phone number](associate-phone-number.md) to it and then call that number\.

## Test chat<a name="test-chat"></a>

Amazon Connect includes a simulated web page that shows how your customers can interact with you, and a Contact Control Panel \(CCP\) that shows the agent experience\. Here's how to test chat:

1. On the navigation menu, choose **Dashboard**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-dashboard-menu.png)

1. Choose **Test chat**\.

   If you don't see the option to test chat, click [here](https://github.com/amazon-connect/amazon-connect-chat-ui-examples#enabling-chat-in-an-existing-amazon-connect-contact-center)\.

1. On the **Test Chat** page, choose **Test Settings**\.

1. Under **System Settings**, choose the contact flow you want to test with chat, and then click **Apply**\. By default, it runs the [Sample inbound flow](sample-inbound-flow.md)\.

1. In the chat window, click the icon as shown below\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-chat-icon.png)

1. Type a message similar to what one of your customers might type\. In the agent window, type a reply\.

1. To see what it's like for an agent to handle multiple chat conversations, copy the dashboard URL into another browser window, and start another chat\. The chat goes to the same instance of the CCP that you already have open\.
**Tip**  
The test environment uses the BasicQueue and Basic Routing Profile\. The Basic Routing Profile is set up for 2 chats\. If you want to test what it's like to have more than two chats, change the Basic Routing Profile to 5 chats\. For instructions, see [Create a routing profile](routing-profiles.md)\. 

   To learn more about what the agent experiences when managing chat conversations, see [Chat with contacts](work-with-chats.md)\. 

## Test tasks<a name="test-tasks"></a>

The first step in testing the task experience is to create a quick connect for the queue you want to assign the example tasks to\. 

**Step 1: Create a quick connect**

1. On the navigation menu, choose **Routing**, **Quick connects**, **Add a new**\.

1. Enter a name for the quick connect\. For example, if you want to assign the test task to yourself, enter your name \(for example, **Jane Doe**\)\.

1. Under **Type**, use the dropdown list to choose **Queue**\.

1. Under **Destination**, use the dropdown list to choose a queue you set up for yourself \(assuming you want to assign the test task to yourself\)\.

1. Under **Contact flow**, choose **Default queue transfer**\.

1. Under **Description**, enter something like **Test quick connect**\.

1. Choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-tasks-quick-connect-setup.png)

**Step 2: Make the quick connect visible in the CCP by assigning it to a queue**

1. After you create the quick connect, go to **Routing**, **Queues** and then choose the appropriate queue for the contact to be routed to\. 

1. On the **Edit queue** page, in the **Quick connects** box, search for the quick connect you created\. For example, it might have your name\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-tasks-janedoe-queue.png)

1. Select the quick connect and then choose **Save**\.

**Step 3: Assign the queue to the agent's routing profile**

1. Go to **Users**, **Routing profiles** and choose the agent's routing profile\. 

1. Under **Set channels and concurrency** choose **Tasks**\.

1. Add the agent's queue to the routing profile, and choose **Task** for the channel\.

   If the agent can receive transfers through other channels, select them as well\.

1. Choose **Save**\.

**Step 4: Test tasks**

1. Open the CCP\. Select the **Task** tab, and then choose **Create task**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-create-task-ccp.png)

   Or, if you're testing the chat experience, for example, you can choose the **Task** icon, as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-chat-task-window.png)

1. Complete the **Create task** page\. When you choose **Assign to**, you can assign only a task to someone or a queue that has quick connect\. 

   To create a scheduled task for the future, use the **Scheduled date/time** box to choose a future date and time\. You can schedule a task up to six days in future\.

   Choose **Create**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-create-task-ccp-2.png)

1. If you chose yourself, the task will be routed to you\. Choose **Accept task**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-tasks-incoming.png)

1. Review the task, and choose **End task** when done\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/test-task-end-task.png)

## View metrics for the test experiences<a name="test-metrics"></a>

When you're testing the voice, chat, and task experiences, you may also want to explore metrics\.

1. On the left navigation menu, choose **Metrics and quality**, **Real\-time metrics**, **Queues**\.

1. You can review the real\-time metrics as you test the different channels\.

1. To view metrics by channel in a real\-time metrics report, go to **Settings**, **Groupings**, **Queues grouped by channels**, **Apply**\. Your report will look similar to the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-rtm-grouping-by-channel.png)