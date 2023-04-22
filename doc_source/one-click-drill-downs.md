# Use one\-click drill\-downs for Routing profiles and Queues tables<a name="one-click-drill-downs"></a>

In real\-time metrics reports, for **Routing profiles** and **Queues** tables, you can open pre\-filtered tables that display the associated queues, routing profiles, or agents\. These one\-click filters provide a way for you to drill into the performance data\.

## Example 1: Queues table \-> Routing profiles table \-> Agents table<a name="one-click-drill-downs-example1"></a>

For example, at a **Queues** table, choose the dropdown and then choose **View routing profiles**, as shown in the following image\.

![\[The real-time metrics report, queues table, dropdown, view routing profiles option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-quick-filter-queue-table.png)

Below the **Queues** table, a **Routing profiles** table appears, as shown in the following image\. It is filtered to display only the routing profiles associated with the queue\. On the **Routing profiles** table, you can choose quick filters to display queues or agents *only associated with that routing profile*\.

![\[The queues table with a box around queue name A, the routing profiles table for queue name A.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-quick-filter-routing-profiles.png)

## Example 2: Queues table \-> Agents table<a name="one-click-drill-downs-example2"></a>

At the **Queues** table, choose **View agents**\. Below the **Queues** table, an **Agents** table appears\. It is filtered to display all the agents working that queue, as shown in the following image\. The agents may be associated with different routing profiles\. 

![\[The queues table, view agents option, the agents table.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-quick-filter-queues-agents.png)