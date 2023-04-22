# Concepts: Tasks in Amazon Connect<a name="tasks"></a>

**Important**  
If you found this page because you need to contact Amazon for support, see [Amazon Customer Service](https://www.amazon.com/gp/help/customer/display.html) \(Amazon orders and deliveries\) or [AWS Support](http://aws.amazon.com/premiumsupport/) \(Amazon Web Services\) instead\.

Amazon Connect Tasks allows you to prioritize, assign, track, and even automate tasks across the disparate tools agents use to support customers\. For example, using Tasks you can:
+ Follow\-up on customer issues recorded in a customer relationship management \(CRM\) solution such as Salesforce\.
+ Follow\-up with a customer through a call\.
+ Complete actions in a business\-specific system, such as processing a customer claim in an insurance application\.

Currently, Amazon Connect Tasks can be used in compliance with [GDPR](http://aws.amazon.com/compliance/gdpr-center) and is approved for SOC, PIC, HITRUST, ISO, and HIPAA\.

## What is a task?<a name="what-is-a-task"></a>

A *task* is a unit of work that an agent must complete\. This includes work that may have originated in external applications\. It's routed, prioritized, assigned, and tracked just like voice and chat\. 

Agents handle tasks in their Contact Control Panel \(CCP\), again just like any other contact\. When assigned a task, agents see a notification with the description of the task, information associated with the tasks, and links to any applications that they might need to complete the task\. The following image shows what an agent's CCP may look like when they manage tasks\.

![\[A task in the contact control panel.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-introduction.png)

## How to create tasks<a name="concepts-set-up-tasks"></a>

Amazon Connect provides different ways for you to create tasks: 

1. You can use pre\-built connectors with CRM applications \(for example, Salesforce and Zendesk\) to automatically create tasks based on a set of pre\-defined conditions, without any custom development\. 

   For example, you can configure a rule in Amazon Connect to automatically create a task when a new case is created in Salesforce\. 

   For more information, see [Set up applications for task creation](integrate-external-apps-tasks.md) and [Create rules that generate tasks for third\-party integrations](add-rules-task-creation.md)\.

1. You can integrate with your homegrown or business\-specific applications to create tasks using Amazon Connect APIs\.

   For more information, see the [StartTaskContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API\.

1. You can add a [Create task](create-task-block.md) block to your flows\. This block enables you to create and orchestrate tasks directly from flows based on customer input \(DTMF input\), and contact and tasks information\.

1. You can enable your agents to create tasks from the Contact Control Panel \(CCP\) without you doing any development work\.

   For example, agents can create tasks to ensure follow up work is not forgotten, such as calling a customer back to provide a status update on their issue\. 

   For more information, see [Test voice, chat, and task experiences](chat-testing.md)\.

For more information on getting started with tasks, see [Set up tasks](concepts-getting-started-tasks.md)\.

## Supported contact flow types<a name="concepts-tasks-supported-contact-flow-types"></a>

You can use tasks in the following flow types:
+ Inbound flow
+ Customer queue flow
+ Agent whisper flow
+ Transfer to queue flow
+ Transfer to agent flow

## Supported contact blocks<a name="concepts-tasks-supported-contact-blocks"></a>

You can use tasks in the following flow blocks:
+ Change routing priority/age
+ Check contact attributes
+ Check hours of operation
+ Check queue status
+ Check staffing
+ Create task
+ Disconnect / hang up
+ Distribute by percentage
+ End flow / resume
+ Get queue metrics
+ Invoke AWS Lambda function
+ Loop
+ Set contact attributes
+ Set customer queue flow
+ Set disconnect flow
+ Set working queue
+ Transfer to flow
+ Transfer to queue
+ Wait

## Linked tasks<a name="linked-tasks"></a>

When using tasks with the [StartTaskContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API, a new contact can be associated with an existing contact through `PreviousContactID` or `RelatedContactId`\. This new contact contains a copy of the [contact attributes](connect-attrib-list.md) from the linked contact\.

The following code shows request syntax that includes `PreviousContactID` and `RelatedContactId`\.

```
PUT /contact/task HTTP/1.1
Content-type: application/json

{
   "Attributes": { 
      "string" : "string" 
   },
   "ClientToken": "string",
   "ContactFlowId": "string",
   "Description": "string",
   "InstanceId": "string",
   "Name": "string",
   "PreviousContactId": "string",
   "QuickConnectId": "string",
   "References": { 
      "string" : { 
         "Type": "string",
         "Value": "string"
      }
   },
   "RelatedContactId": "string",
   "ScheduledTime": number,
   "TaskTemplateId": "string"
}
```

When you use `PreviousContactID` or `RelatedContactID` to create tasks, note the following:
+ `PreviousContactID` \- When contacts are linked using the `PreviousContactID`, updates that are made to contact attributes at any time in the chain will percolate through the entire chain\.

  There can be a maximum of 12 linked contacts in a chain\.
+ `RelatedContactID` \- When contacts are linked using the `RelatedContactID`, updates that are made to contact attributes will percolate only to the contactID that is referenced in the [UpdateContactAttributes](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactAttributes.html) API\. 

  The limit of 12 contacts in a chain does not apply when you use `RelatedContactID` to create a task\.

**Note**  
You can specify only `PreviousContactID` or `RelatedContactID` in a request body, but not both\. If you do specify both, Amazon Connect returns an `InvalidRequestException` error with a 400 status code\.

For information about how `PreviousContactID` and `RelatedContactId` are modeled in contact records, see [ContactTraceRecord](ctr-data-model.md#ctr-ContactTraceRecord) in the contact records data model\.

## Using IAM? Add Task permissions<a name="iam-tasks"></a>

If your organization is using custom [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) policies to manage access to the Amazon Connect console, make sure users have the appropriate permissions to set up applications for task creation\. For a list of required permissions, see [Tasks page](security-iam-amazon-connect-permissions.md#tasks-page)\.

**Note**  
If your instance was created before October 2018, for information about how to configure your service\-linked roles \(SLR\), see [For instances created before October 2018](connect-slr.md#migrate-slr)\.

## Track tasks in real\-time and historical metrics reports<a name="tracking-tasks"></a>

You can track the status of all tasks in real\-time and historical metrics reports, just like you track contacts in other channels\. For example, you can track:
+ How long agents spent working on each task \([Agent on contact time](historical-metrics-definitions.md#agent-on-contact-time-historical)\)\.
+ The total time from when a task was created to when it was completed\. \([Contact handle time](historical-metrics-definitions.md#contact-handle-time-historical)\)\.

There are a few metrics that don't apply to tasks so you'll notice a value of 0 on the report for them:

**Real\-time metrics**
+ [Avg interaction and hold time](real-time-metrics-definitions.md#average-interaction-hold-time-real-time)
+ [Avg hold time](real-time-metrics-definitions.md#average-hold-time-real-time)

**Historical metrics**
+ [Agent interaction and hold time](historical-metrics-definitions.md#agent-interaction-hold-time-historical)
+ [Agent interaction time](historical-metrics-definitions.md#agent-interaction-time-historical)
+ [Average agent interaction time](historical-metrics-definitions.md#average-agent-interaction-time-historical)
+ [Average customer hold time](historical-metrics-definitions.md#average-customer-hold-time-historical)

### Manage tasks to custom service levels \(SL\)<a name="tasks-custom-sl"></a>

While voice and chats may have short service level times based on seconds or minutes, you may have some tasks with service levels that are hours or days\. You can create custom service level durations that are appropriate to each of your channels\. For more information, see [real\-time custom service levels](real-time-metrics-definitions.md#custom-service-level-real-time) and [historical custom service levels](historical-metrics-definitions.md#custom-service-level-historical)\. 

## When do tasks end?<a name="when-do-tasks-end"></a>

The total duration of a task can be up to 7 days\. A task ends when one of the following happens: 
+ An agent completes the task\.
+ A flow runs a [Disconnect / hang up](disconnect-hang-up.md) block, which ends the task\.
+ A task reaches the 7 day limit\.
+ You end the task using the [StopContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContact.html) API\.

## Search and review completed tasks<a name="task-ctr-fields"></a>

Use the [Contact search](contact-search.md) page to search for and review completed tasks\. 

The following image is an example of what the **Contact Summary** and **References** look like in a contact record for a task\.

![\[A contact record page for a task.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-sample-ctr.png)

The following data is appended to the contact record but not stored with it\. The data is included in an export\. 
+ Flow ID
+ Potential attributes:
  + [ContactDetails](ctr-data-model.md#ctr-contact-details)
    + Name: the name of the task
    + Description: the description of the task
  + [References](ctr-data-model.md#ctr-contact-references): any links to forms or other sites

When task is scheduled for a future date and time, **Contact Summary** also displays **Scheduled time**\.

## More information<a name="tasks-more-information"></a>
+ [Amazon Connect feature specifications](feature-limits.md)
+ [Accept a task](accept-task.md)
+ [Create a new task](create-task.md)
+ [Transfer a task](transfer-task.md)