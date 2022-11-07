# Create Amazon Connect rules<a name="connect-rules"></a>

A rule is an action that Amazon Connect automatically performs, based on conditions you specify\. Contact center managers, supervisors and QA analysts can quickly create rules from the Amazon Connect console\. No coding is required\.

The following image shows the Rules user interface, and the actions available when you create a rule\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-action-no-wisdom.png)

By creating rules, you can:
+ Automatically categorize contacts\.
+ Send notifications about customer escalations\.
+ Display tips in the agent application\.
+ Assign supervisor tasks based on customer conversations\.

Rules allow you to automate common and repeatable actions required for quality assurance, workforce management, and customer engagement\. These actions are automated based on pre\-defined trigger conditions that you define, such as keywords used on a contact, sentiment trend of a contact, frequent interruptions by agent on a contact, agents being silent for long\-periods on a contact, filtering specific contact attributes or queues, and more\. 

## Common usage scenarios<a name="rules-scenarios"></a>
+ For Contact Lens, you can create rules to automatically categorize contacts based on keywords and phrases uttered by the agent or the customer\. You can also use rules with real\-time contact lens to alert supervisors in real\-time when a critical customer experience issue occurs and the agent requires live assistance\. 
+ For coaching and escalation scenarios, you can create rules to automatically categorize contacts that are not meeting your compliance requirements and assign tasks for the agents to go through a certain training program on your organization's compliance policy\.

## Third\-party integrations<a name="rules-overview-integrations"></a>

Rules also provide third\-party integrations with Contact Relationship Management \(CRM\) and IT service management \(ITSM\) vendors, such as Salesforce and Zendesk\.

For example, you can create rules for whenever a new case or ticket is created in the Salesforce CRM or Zendesk ticket management system\. You can set up the rule to automatically assign tasks to agents or supervisors based on the new case or ticket created, and to alert them to take necessary action\. If you want to use email notification, you can automatically generate an EventBridge event that runs a custom email notification application to alert agents or supervisors\. This enables contact center managers to integrate their existing CRM and ITSM solutions with Amazon Connect through rules, and to monitor the creation of new cases or tickets through tasks\. 

## More information<a name="rules-more-information"></a>
+ [Alert supervisors in real\-time based on keywords and phrases](add-rules-for-alerts.md)
+ [Automatically categorize contacts based on uttered keywords and phrases](rules.md)
+ [Create a task when a contact is categorized in real\-time or post\-call](contact-lens-rules-create-task.md)
+ [Create a Contact Lens rule that generates an EventBridge event](contact-lens-rules-eventbridge-event.md)
+ [Create rules that generate tasks for third\-party integrations](add-rules-task-creation.md)