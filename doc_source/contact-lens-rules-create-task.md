# Create a task when a contact is categorized in real\-time or post\-call<a name="contact-lens-rules-create-task"></a>

An especially powerful use of Content Lens rules is to build rules that generate tasks\. This helps you identify issues in your contact center for you to follow up, and creates traceable actions with owners\. Following are some examples:
+ Create a task to review a contact when the customer is fraudulent\. For example, you can create a follow\-up task when a customer utters words or phrases that makes them appear potentially fraudulent\.
+ Follow up when the customer mentions specific topics that you want to later on upsell or provide additional support by reaching out\.
+ Follow up when there is a serious quality issue\. In addition to contacts being categorized and getting alerts, you can route a task so you have owners\. You also have contact records for these tasks, so you can search for and trace them\. 

**To create a rule that creates a task**

1. When you create your rule, choose **Create Task** for the action\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-add-task-example1.png)

1. Complete the task fields as follows:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-add-tasks-example2.png)

   1. **Category name**: The category name appears in the contact record\. Max length: 200 characters\.

   1. **Name**: The name appears in the agent's Contact Control Panel \(CCP\)\. Max length: 512 characters\. 

   1. **Description**: The description appears in the agent's Contact Control Panel \(CCP\)\. Max length: 4096 characters\.
**Tip**  
In **Name** and **Description**, use \[ \] to choose from a menu of dynamic values\. For more information, see [Create a task when a contact is categorized in real\-time or post\-call](#contact-lens-rules-create-task)\.   

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-add-tasks-brackets.png)

   1. **Task reference name**: This is a default reference that automatically appears in the agent's CCP\.
      + For real\-time rules, the task reference links to the Real\-time details page\. 
      + For post\-call rules, the task reference links to the **Contact record details** page\. 

   1. **Additional Reference name**: Max length: 4096 characters\. You can add up to 25 references\.

   1. **Select a contact flow**: Choose the contact flow that is designed to route the task to the appropriate owner of the task\. The contact flow must be saved and published for it to appear in your list of options in the dropdown\.

1. The following image shows an example of how this information appears in the agent's CCP:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-add-tasks-ccp.png)

   In this example, the agent sees the following values for **Name**, **Description**, and **Task reference name**:

   1. **Name** = Action\-Required\-Contact Lens \- ba2cf8fe\.\.\.\. 

   1. **Description** = Test

   1. **Task reference name** = taskRef and the URL to the Real\-time details page

1. Choose **Next**\. Review and then choose **Save** the task\. 

1. After you add rules, they are applied to new contacts that occur after the rule was added\. Rules are applied when Contact Lens analyzes conversations\.

   You cannot apply rules to past, stored conversations\. 

## Voice and task contact records are linked<a name="rules-voice-task-ctrs"></a>

When a rule creates a task, a contact record is automatically generated for the task\. It's linked to the contact record of the voice call that met the criteria for the rule to create the task\.

For example, a call comes into your contact center and generates CTR1:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-attributes-example1.png)

The Rules engine generates a task\. In the contact record for the task, the voice contact record appears as the **Previous contact ID**\. In addition, the task contact record inherits contact attributes from the voice contact record, as illustrated in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-attributes-example2.png)

## About dynamic values for ContactId, AgentId, QueueId, RuleName<a name="rules-task-attributes"></a>

The dynamic values in brackets \[ \] are called [contact attributes](what-is-a-contact-attribute.md)\. Contact attributes enable you to store temporary information about the contact so you can use it in a contact flow\.

When you add contact attributes in brackets \[ \] — such as ContactId, AgentId, QueueId, or RuleName — the value is passed from one contact record to another\. You can use contact attributes in your contact flow to branch and route the contact accordingly\.

For more information, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\.