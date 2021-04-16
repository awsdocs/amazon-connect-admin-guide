# Disassociate an Amazon Connect connection<a name="disassociate-connection"></a>

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