# Set up application integration for Zendesk<a name="integrate-zendesk-tasks"></a>

## Step 1: Enable the events connector for Amazon EventBridge<a name="enable-zendesk-in-eventbridge"></a>

If you don't already have the EventBridge connector for Zendesk enabled, you need to set it up first\. Otherwise, go to [Step 2: Integrate Zendesk with Amazon Connect for task creation](#steps-integrate-zendesk)\. 

1. Copy your AWS account number: 

   1. In the Amazon EventBridge console, go to **Partner event sources**\.

   1. Search for or scroll to **Zendesk**, and choose **Set up**\.

   1. Choose **Copy** to copy your AWS account information\.

1. Go to [Setting up the events connector for Amazon EventBridge](https://support.zendesk.com/hc/en-us/articles/360043496933-Setting-up-the-events-connector-for-Amazon-EventBridge) in the Zendesk Help and follow the instructions\.

## Step 2: Integrate Zendesk with Amazon Connect for task creation<a name="steps-integrate-zendesk"></a>

**Note**  
If you use custom AWS Identity and Access Management \(IAM\) policies, for a list of the required IAM permissions to set up Amazon Connect Tasks, see [Tasks page](security-iam-amazon-connect-permissions.md#tasks-page)\.

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. Choose **Tasks**, and then choose **Add an application**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-add-an-application-button.png)

1. On the **Select application** page, choose **Zendesk**\. 

1. After you choose to integrate with Zendesk, the application requirements are listed on the page\.

   The following image shows the requirements for Zendesk\. In this procedure, we walk you through the steps to select the "Support ticket" event type in Zendesk\. Acknowledge the steps and choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-choose-an-app-zendesk.png)

1. On the **Establish connection** page, choose one of the following: 
   + **Use an existing connection**\. This allows you to reuse existing EventBridge resources you may have created in your AWS account\.
   + **Create a new connection**: Enter the information required by the external application\.

     1. Enter your application instance URL\. This URL is used for deep\-linking into the tasks created in your external application\.

     1. Provide a friendly name for your connection, for example, **Zendesk \- Test instance**\. Later, when you [add rules](add-rules-task-creation.md), you'll refer to this friendly name\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-zendesk.png)

1. Choose **Copy** to copy your AWS account ID, and then choose **Login to Zendesk**\. This takes you away from the **Establish connection** page for now, but you return to it shortly\.

1. After you're logged in to Zendesk, choose **Connect** to connect the Events Connector for Amazon EventBridge\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-connect-zendesk-eventbridge.png)

1. In Zendesk, on the **Amazon Web Services** page, paste in your Amazon Web Service account ID, choose your Region, choose **Support ticket**, acknowledge the terms of use, and the choose **Connect**\. Zendesk creates a resource in Amazon EventBridge\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-connect-zendesk-support-ticket.png)

1. Return to the **Establish connection** page in Amazon Connect choose **Next**\.

1. On the **Establish** page, you'll see the message that Amazon Connect has successfully connected with Zendesk\. Choose **Next**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-final-zendesk.png)

1. On the **Review and integrate** page, check that the **Connection status** says **Connected**, and then choose **Complete integration**\. 

   This creates a connection that associates the EventBridge resource for Zendesk to Amazon Connect\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-review-and-integrate-zendesk.png)

1. On the **Tasks** page, the new connection is listed\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-final2-zendesk.png)

You're done\! Next, add rules that tell Amazon Connect when to create a task and how to route it\. For instructions, see [Create rules that generate tasks for third\-party integrations](add-rules-task-creation.md)\.

## What to do when is a connection isn't successfully established<a name="fix-connection-not-established-zendesk"></a>

A connection might fail to create a task if you do not correctly select the **Support ticket** event type when setting up the connection in Zendesk, after being prompted to do so in the flow\. To fix this, log in to Zendesk, and update that setting, as shown in the following image\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/zendesk-support-ticket.png)

There is also another case where you may not have selected the correct AWS Region that the Amazon Connect instance is in, when setting up EventBridge\. To fix:

1. Go to the EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. Disconnect your EventBridge connection\.

1. In the Amazon Connect console, restart the flow\.