# Create rules that generate tasks for third\-party integrations<a name="add-rules-task-creation"></a>

After you set up an external application to generate tasks automatically, you need to build rules that tell Amazon Connect when to create tasks, and how to route them\.

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for **Rules** permissions\.

1. In Amazon Connect, on the navigation menu, choose **Rules**\.

1. On the **Rules** page, use the **Create a rule** dropdown list to choose **External application**\.

1. At the **Trigger and conditions** page, assign a name to the rule\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules.png)

1. Choose the event that will generate a task, and the instance of the external application where the event must occur\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-add-rule-for-zendesk.png)

   1. Select the instance for the external application\.

   1. Choose the conditions that must be met to generate the task\.

1. Choose **Next**\.

1. On the **Action** page, specify the task to be generated when the rule is met\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/task-rule-action-to-take.png)

   1. The description of the task appears to the agent in their Contact Control Panel \(CCP\)\.

   1. The task reference name appears to the agent as a link to the specified URL\.

1. Choose **Save**\.

## Test the rule<a name="test-rules-task-creation"></a>

1. Go the external application and create the event that initiates the action\. For example, in Zendesk, create a ticket that's type **Question**\. 

1. Go to **Analytics**, **Contact search**\. 

1. Under **Channel**, choose **Task**, and then choose **Search**\.

1. Verify the task was created\.