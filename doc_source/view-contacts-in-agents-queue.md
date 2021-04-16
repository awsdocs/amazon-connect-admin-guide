# View how many contacts are in an agent's queue<a name="view-contacts-in-agents-queue"></a>

To see how many contacts are in an agent's personal queue, add an **Agent queues** table to your **Real\-time metrics**, **Queues** report\. Then view these two metrics: 
+ **In Queue**—how many contacts are in an agent's personal queue\.
+ **Queued**—the number of contacts added to their personal queue during the specified time range\.

Use the following procedure\. 

1. Go to **Metrics and quality**, **Real\-time metrics**, **Queues\.**

1. Choose **New table**, **Agent queues**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-agent-queues.png)

   The **In queue** column displays how many contacts are in the agent's queue\.

1. Review the metrics in then **In queue** and **Queue** columns\.
**Tip**  
An agent is included in the **Agent queues** table only if they are online or there is at least one contact in the their queue\.

## Add In Queue and Queue to the Agent queue table<a name="add-in-queue-to-agent-table"></a>

If **In queue** or **Queue** don't appear in your **Agent queue** table, use the following steps to add them\.

1. On the **Agent queues** table, choose **Settings**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-settings2.png)

1. Choose the **Metrics** tab\.

1. Scroll to the **Performance** section and choose **In queue** and **Queue**, and then **Apply**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-metrics-in-queue.png)

   The changes appear in your table immediately\.

1. Choose **Save** to add this report to your list of Saved reports\. 