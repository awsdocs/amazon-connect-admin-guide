# Queues: standard and agent<a name="concepts-queues-standard-and-agent"></a>

There are two types of queues:
+ **Standard queues**: This is where contacts wait before they are routed to and accepted by agents\.
+ **Agent queues**: These queues are created automatically when you add an agent to your contact center\.

  Contacts are only routed to agent queues when explicitly sent there as part of a flow\. For example, you might route contacts to a specific agent who's responsible for certain customer issues, such as billing or premium support\. Or you might use agent queues to route to an agent's voice\-mail\. 

Contacts waiting in agent queues are higher priority than contacts waiting in standard queues\. Contacts in agent queues have the highest priority and zero delay: 
+ Highest priority: If there's another contact in the basic queue, Amazon Connect chooses to give the agent the contact from the agent queue first\.
+ Zero delay: If the agent is available, the contact immediately gets routed to them\.

## Queues in metrics reports<a name="concepts-queues-in-reports"></a>

In a [real\-time metrics report](real-time-metrics-reports.md), you can monitor how many contacts are in standard queues and agent queues\. The following image shows a sample real\-time metrics Queues report where an Agents table and Agents queues table have been added\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-standard-and-agent-queues.png)

When an agent gets a contact from a standard queue, the contact never appears in the agent queue\. It just goes directly to the agent\. 

In a [historical metrics report](historical-metrics.md), by default agent queues don't appear in a Queues table\. To show them, choose the **Settings** icon, then choose **Show agent queues**\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-queues-settings-agent-queues.png)

**Tip**  
The metrics APIs don't support agent queues\.

## Default queue: BasicQueue<a name="concepts-default-queue"></a>

Amazon Connect includes a default queue named **BasicQueue**\. Along with the [default flows](contact-flow-default.md) and default routing profile \(named **Basic routing profile**\), it powers your contact center so you don't need to do any customization\. This is what enables you to get started quickly\. 