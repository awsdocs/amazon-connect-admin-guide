# Tasks<a name="tasks"></a>

Amazon Connect Tasks allows you to prioritize, assign, track, and even automate tasks across the disparate tools agents use to support customers\. For example, using Tasks you can:
+ Follow\-up on customer issues recorded in a customer relationship management \(CRM\) solution such as Salesforce\.
+ Follow\-up with a customer via a call\.
+ Complete actions in a business\-specific system, such as processing a customer claim in an insurance application\.

## What is a task?<a name="what-is-a-task"></a>

A *task* is a unit of work that an agent must complete\. This includes work that may have originated in external applications\. It's routed, prioritized, assigned, and tracked just like voice and chat\. 

Agents handle tasks in their Contact Control Panel \(CCP\), again just like any other contact\. When assigned a task, agents see a notification with the description of the task, information associated with the tasks, and links to any applications that they might need to complete the task\. The following image shows what an agent's CCP may look like when they manage tasks\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-introduction.png)

## How to create tasks<a name="concepts-set-up-tasks"></a>

Amazon Connect provides different ways for you to create tasks: 

1. You can use pre\-built connectors with CRM applications \(for example, Salesforce and Zendesk\) to automatically create tasks based on a set of pre\-defined conditions, without any custom development\. 

   For example, you can configure a rule in Amazon Connect to automatically create a task when a new case is created in Salesforce\. 

   For more information, see [Set up applications for task creation](integrate-external-apps-tasks.md) and [Add rules for task creation](add-rules-task-creation.md)\.

1. You can integrate with your homegrown or business\-specific applications to create tasks using Amazon Connect APIs\.

   For more information, see the [StartTaskContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API\.

1. You can enable your agents to create tasks from the Contact Control Panel \(CCP\) without you doing any development work\.

   For example, agents can create tasks to ensure follow up work is not forgotten, such as calling a customer back to provide a status update on their issue\. 

   For more information, see [Test voice, chat, and task experiences](chat-testing.md)\.

## Get started with tasks<a name="concepts-set-up-tasks"></a>

1. [Update your agent's routing profile](routing-profiles.md) so they can manage and create tasks\.

   When you add tasks to their routing profile, you can specify that up to 10 tasks be assigned to them at a time\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-routing-profile-2.png)

1. [Create quick connects](quick-connects.md) so that agents can create/assign tasks to themselves, or other agents or shared queues\.

1. Update your contact flows to route tasks\.

1. Optionally, [integrate with external applications](integrate-external-apps-tasks.md) and [set up rules to automatically create tasks](add-rules-task-creation.md) based on pre\-defined conditions\.

### Supported contact flow types<a name="concepts-tasks-supported-contact-flow-types"></a>

You can use tasks in the following contact flow types:
+ Inbound contact flow
+ Customer queue flow
+ Agent whisper flow
+ Transfer to queue contact flow
+ Transfer to agent flow

### Supported contact blocks<a name="concepts-tasks-supported-contact-blocks"></a>

You can use tasks in the following contact blocks:
+ Change routing priority/age
+ Check contact attributes
+ Check hours of operation
+ Check queue status
+ Check staffing
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

## When do tasks end?<a name="when-do-tasks-end"></a>

The total duration of a task can be up to 7 days\. A task ends when one of the following happens: 
+ An agent completes the task\.
+ A contact flow runs a [Disconnect / hang up](disconnect-hang-up.md) block, which ends the task\.
+ A task reaches the 7 day limit\.
+ You end the task using the [StopContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContact.html) API\.

## Search and review completed tasks<a name="task-ctr-fields"></a>

Use the [Contact search](contact-search.md) page to search for and review completed tasks\. 

Following is an example image of what the **Contact Summary** and **References** look like in a contact trace record \(CTR\) for a task\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-sample-ctr.png)

The following data is appended to the CTR but not stored with it\. The data is included in an export\. 
+ Contact flow ID
+ Potential attributes:
  + [ContactDetails](ctr-data-model.md#ctr-contact-details)
    + Name: the name of the task
    + Description: the description of the task
  + [References](ctr-data-model.md#ctr-contact-references): any links to forms or other sites

## More information<a name="tasks-more-information"></a>
+ [Feature specifications](amazon-connect-service-limits.md#feature-limits)
+ [Accept a task](accept-task.md)
+ [Create a new task](create-task.md)
+ [Transfer a task](transfer-task.md)