# Set up applications for task creation<a name="integrate-external-apps-tasks"></a>

You can set up applications for task creation in just a few steps, no coding required\. Amazon Connect uses Amazon EventBridge to pull data from your external application\. 

If you integrate with Salesforce for event creation, Amazon Connect also uses Amazon AppFlow to put the data into EventBridge\. This is because of how Salesforce sends events through the Amazon AppFlow APIs\. To learn more about how Amazon Connect uses EventBridge and Amazon AppFlow resources to power Salesforce integrations, see this blog post: [ Building Salesforce integrations with Amazon EventBridge and Amazon AppFlow](https://aws.amazon.com/blogs/compute/building-salesforce-integrations-with-amazon-eventbridge/)\. 

**Note**  
If you use custom AWS Identity and Access Management \(IAM\) policies, for a list of the required IAM permissions to set up Amazon Connect Tasks, see [Tasks page](security-iam-amazon-connect-permissions.md#tasks-page)\.

**To integrate external applications for task creation**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. Choose **Tasks**, and then choose **Add an application**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-add-an-application-button.png)

1. On the **Select application** page, choose the external application you want to use to generate events\. 

   For the remaining steps, see the following instructions for your application:
   + [Set up application integration for Salesforce](#integrate-salesforce-tasks)
   + [Set up application integration for Zendesk](#integrate-zendesk-tasks)

## Set up application integration for Salesforce<a name="integrate-salesforce-tasks"></a>

1. Review the application requirements that are listed on the **Select application** page\. 

   The following image shows the requirements for Salesforce\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-choose-an-app-salesforce.png)

   1. To verify that Salesforce is compatible with Amazon AppFlow, log in to Salesforce, for example, https://\[instance\_name\]\.my\.saleforce\.com\.
**Important**  
Verify that you have enabled **Change Data Capture** in Salesforce\. The following image shows an example **Change Data Capture** page in Salesforce where you select the Case entities:  

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-verify-app-salesforce.png)

1. After you verify Salesforce requirements, on the **Select application** page, choose **Next**\.

1. On the **Establish connection** page, choose one of the following: 
   + **Use an existing connection**\. This allows you to reuse existing EventBridgeresources that are linked to Amazon AppFlow flows that you may have created in your AWS account\. 
   + **Create a new connection**: Enter the information required by the external application\.

     1. Enter your application instance URL\. This URL is used for deep\-linking into the tasks created in your external application\.

     1. Provide a friendly name for your connection, for example, **Salesforce \- Test instance**\. Later, when you [add rules](add-rules-task-creation.md), you'll refer to this friendly name\.

     1. Specify whether this is a production or sandbox environment\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection.png)

1. Choose **Log in to Salesforce**\. 

1. In Salesforce, choose to allow access to Amazon Connect Embedded Login App \[Region\]\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-allow-access-salesforce.png)

1. After Amazon Connect has successfully connected with the Salesforce, go to Salesforce and verify that the refresh token policy for Amazon Connect Embedded Login App is set to **Refresh token is valid until revoked**\. This grants Amazon AppFlow access to pull data from your Salesforce account without re\-authenticating\.

1. On the **Establish connection** page, select the box shown in the following image, and choose **Next**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-successful.png)

1. On the **Review and integrate** page, check that the **Connection status** says **Connected**, and then choose **Complete integration**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-review-and-integrate.png)

1. On the **Tasks** page, the new connection is listed\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-establish-connection-final.png)

You're done\! Next, add rules that tell Amazon Connect when to create a task and how to route it\. For instructions, see [Add rules for task creation](add-rules-task-creation.md)\.

## Set up application integration for Zendesk<a name="integrate-zendesk-tasks"></a>

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

You're done\! Next, add rules that tell Amazon Connect when to create a task and how to route it\. For instructions, see [Add rules for task creation](add-rules-task-creation.md)\.

## What to do when is a connection isn't successfully established<a name="fix-connection-not-established"></a>

### Salesforce<a name="fix-connection-not-established-salesforce"></a>

In the case of Salesforce, a connection might fail to be established for Salesforce if you didn’t follow the instructions next to the check boxes to verify that it's compatible with Amazon AppFlow\.

A common error is not setting up the **Case** entity in the **Change Data Capture** settings to capture these events\. To fix:

1. Log in to Salesforce, go to the **Change Data Capture**, and select the Case entity\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-verify-app-salesforce.png)

1. Open the Amazon AppFlow console at [https://console\.aws\.amazon\.com/appflow\)](https://console.aws.amazon.com/appflow) to select the flow that was just created, and then choose **Activate flow**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-integration-activate-flow.png)

Alternatively, you might need to delete the Amazon AppFlow Salesforce connection and flow, and start again\. 

### Zendesk<a name="fix-connection-not-established-zendesk"></a>

A connection might fail to create a task if you do not correctly select the **Support ticket** event type when setting up the connection in Zendesk, after being prompted to do so in the flow\. To fix this, log in to Zendesk, and update that setting, as shown in the following image\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/zendesk-support-ticket.png)

There is also another case where you may not have selected the correct AWS Region that the Amazon Connect instance is in, when setting up EventBridge\. To fix:

1. Go to the EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. Disconnect your EventBridge connection\.

1. In the Amazon Connect console, restart the flow\.

## Monitor task creation<a name="monitor-task-creation"></a>

After your connection is established, if it stops working, in Amazon Connect disassociate the connection, and then re\-establish it\. If that doesn't solve the issue, do the following:

**Zendesk**

1. Go to the EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. Check the status of the event source connection to see if it is active\.

**Salesforce**

1. Go to the Amazon AppFlow console at [https://console\.aws\.amazon\.com/appflow\)](https://console.aws.amazon.com/appflow)\. 

1. Monitor the flow that was created for the account that was set up\.

The following image shows what a flow looks like in the Amazon AppFlow console for Salesforce\. It contains information about the status of the connection, and when it was last run\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/salesforce-appflow-flow.png)

For both Zendesk and Salesforce, you can go to the EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/) to see your connection state and see if it is active, pending, or deleted\. 

The following image shows an example EventBridge console\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/eventbridge-zendesk-salesforce-connection-health.png)

## Disassociate an Amazon Connect connection<a name="disassociate-connection"></a>

At any time you can disassociate a connection, and stop the automatic generation of tasks based on events from the external application\. 

**To stop the automatic generation of tasks**

1. Choose the application, and then choose **Remove connection**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-disconnect-connection.png)

1. Type **Remove**, and then choose **Remove**\. 

   If you need to debug, you are still able to go to Amazon AppFlow \(Salesforce\) or EventBridge\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-disconnect-2.png)

**To remove the connection altogether from Zendesk**

1. Log in to Zendesk, and navigate to **https://\[subdomain\]\.zendesk\.com/admin/platform/integrations**\. 

1. Disconnect the EventBridge connection\.

**To remove the connection altogether from Salesforce**
+ Open the Amazon AppFlow console at [https://console\.aws\.amazon\.com/appflow](https://console.aws.amazon.com/appflow), and delete the Salesforce connection and flow that were created in Amazon Connect\. 

  Flows are created with the name pattern of amazon\-connect\-salesforce\-to\-eventbridge\-\[subdomain\]\.

  Connections are created with the name pattern of amazon\-connect\-salesforce\-\[subdomain\]

To re\-enable the automatic generation of tasks, repeat the setup steps\. 