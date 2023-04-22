# About queued callbacks in metrics<a name="about-queued-callbacks"></a>

This topic explains how queued callbacks appear in your real\-time metrics reports and the contact record\.

**Tip**  
To see only the number of customers who are waiting for a call back, you need to create a queue that only takes callback contacts\. To learn how to do this, see [Set up routing](connect-queues.md)\. Currently there isn't a way to see the phone numbers of the contacts waiting for callbacks\.

1. Callbacks are initiated when the [Transfer to queue](transfer-to-queue.md) block is triggered to create the callback in a callback queue\. The following image of a flow shows the **Transfer to queue** block at the end of the flow\.  
![\[A flow with the Transfer to queue block at the end.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/queued-callback-flow-callback-initiation.png)

1. After any initial delay is applied, the callback is put into the queue\. It remains there until an agent is available and can be offered the contact\. The following image shows the contact in the **In queue** column on the **Real\-time metrics** page\.  
![\[A contact listed in the In queue column on the real-metrics page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-callback-in-queue.png)

1. When the callback is connected to the agent, a new contact record is created for the contact\. The following diagram shows three contact records\. The third record is for the callback, connected to Agent 3\.  
![\[Three blocks, one for each contact record.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-diagram.png)

1. The **Initiation Timestamp** in the callback contact record corresponds to when the callback is initiated in the flow, shown in step 1\. The following image shows the **Initiation Timestamp** field on the **Contact Record** page\.  
![\[The contact record page, the Initiation Timestamp field.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-callback-initiation-timestamp.png)

## How properties in the Transfer to Queue block affect this flow<a name="transfer-to-queue-properties"></a>

The [Transfer to queue](transfer-to-queue.md) block has the following properties, which affect how Amazon Connect handles the callback:
+ **Initial delay**: This property affects when a callback is put in queue\. Specify how much time has to pass between a callback contact being initiated in the flow, and the customer being put in queue for the next available agent\. For more information, see [How Initial delay affects Scheduled and In queue metrics](scheduled-vs-inqueue.md)\. 
+ **Maximum number of retries**: If this is set to 2, then Amazon Connect tries to call the customer at most three times: the initial callback, and two retries\. 
+ **Minimum time between attempts**: If the customer doesn't answer the phone, this is how long to wait before trying again\. 