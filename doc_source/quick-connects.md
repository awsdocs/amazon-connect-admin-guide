# Create quick connects<a name="quick-connects"></a>

Quick connects are a way for you to create a list of destinations for common transfers\. For example, you might create a quick connect for Tier 2 support\. If agents in Tier 1 support can't solve the issue, they will transfer the contact to Tier 2\. 

## Types of quick connects<a name="quick-connect-types"></a>

The type of a quick connect specifies the destination\. You can specify one of the following destinations\.

### External quick connect<a name="external-quick-connect-type"></a>

Contacts are transferred to an external number \(such as an on\-call pager\)\. 

### Agent quick connect<a name="agent-quick-connect-type"></a>

Contacts are transferred to a specific agent as part of a contact flow\.

**Important**  
Agent and Queue quick connects only appear in the CCP when an agent goes to transfer a contact\. 

### Queue quick connect<a name="queue-quick-connect-type"></a>

Contacts are transferred to a queue as part of a contact flow\.

**Important**  
Agent and Queue quick connects only appear in the CCP when an agent goes to transfer a contact\. 

## Step 1: Create quick connects<a name="step1-create-quick-connects"></a>

 Following are the instructions to add quick connects manually using the Amazon Connect console\. To add quick connects programmatically, use the [CreateQuickConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateQuickConnect.html) API\.

**To create a quick connect**

1. On the navigation menu, choose **Routing**, **Quick connects**, **Add new**\.

1. Enter a name for the connect\. Choose the type, and then specify the destination \(such as a phone number or the name of an agent\), contact flow \(if applicable\), and description\.

1. To add more quick connects, choose **Add new**\.

1. Choose **Save**\.

## Step 2: Enable agents to see quick connects<a name="step2-enable-agents-to-see-quick-connects"></a>

**To enable your agents to see the quick connects in the CCP when they transfer a contact**

1. After you create the quick connect, go to **Routing**, **Queues** and then choose the appropriate queue for the contact to be routed to\.

1. On the Edit queue page, in the Quick connect box, search for the quick connect you created\.

1. Select the quick connect and then choose **Save**\.

**Tip**  
Agents see all of the quick connects for the queues associated with their routing profile\.

## Example: Create an external quick connect to a mobile phone<a name="example-create-external-quick-connect"></a>

In this example, you create an external quick connect to a person's mobile phone\. This might be for a supervisor, for example, so agents can call them if needed\.

**Create a quick connect for a person's mobile phone number**

1. On the navigation menu, choose **Routing**, **Quick connects**, **Add new**\.

1. Enter a name for the quick connect, for example, **John Doe's cell phone**\.

1. For **Type**, select **External**\.

1. For **Destination**, enter the mobile phone number, starting with the country code\. In the US, the country code is 1, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/quick-connect-johndoe.png)

1. Choose **Save**\.

**Add the quick connect to a queue\. Agents working this queue will see the quick connect in their CCP\.**

1. Go to **Routing**, **Queues**, and choose the queue you want to edit\.

1. On the **Edit queue** page, in **Outbound caller ID number**, choose a number claimed for your contact center\. This is required to make outbound calls\.

1. At the bottom of the page, in the **Quick connect** box, search for the quick connect you created, for example, **John Doe's cell phone**\.

1. Select the quick connect and then choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/quick-connect-johndoe-queue.png)

**Test the quick connect**

1. Open the Contact Control Panel\.

1. Choose **Quick connects**\.

1. Select the quick connect you created, and then choose **Call**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/quick-connect-johndoe-call.png)