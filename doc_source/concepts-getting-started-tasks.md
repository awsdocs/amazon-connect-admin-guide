# Set up tasks<a name="concepts-getting-started-tasks"></a>

1. [Update your agent's routing profile](routing-profiles.md) so they can manage and create tasks\.

   When you add tasks to their routing profile, you can specify that up to 10 tasks be assigned to them at a time\. The following image shows the **Tasks** option on the **Routing profile** page\.  
![\[The Tasks option, max tasks per agent set to 5, queue set to voice, chat, task.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-routing-profile-2.png)

1. [Create quick connects](quick-connects.md) so that agents can create/assign tasks to themselves, or other agents or shared queues\.

1. Update your flows to route tasks\.

1. Optionally, [create task templates](task-templates.md) to make it easy for agents to create tasks\. All the fields they need to create a task are defined for them\.

1. Optionally, [integrate with external applications](integrate-external-apps-tasks.md) and [set up rules to automatically create tasks](add-rules-task-creation.md) based on pre\-defined conditions\.

1. By default all agents can create tasks\. If you want to block [permissions](task-template-permissions.md) for some agents, assign the **Contact Control Panel**, **Restrict task creation permission** in their security profile\.