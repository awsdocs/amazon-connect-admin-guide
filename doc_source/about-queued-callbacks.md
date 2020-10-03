# About queued callbacks in metrics<a name="about-queued-callbacks"></a>

This topic explains how queued callbacks appear in your real\-time metrics reports and the contact trace record \(CTR\)\.

**Tip**  
To see only the number of customers who are waiting for a call back, you need to create a queue that only takes callback contacts\. To learn how to do this, see [Set up routing](connect-queues.md)\. Currently there isn't a way to see the phone numbers of the contacts waiting for callbacks\.

1. Callbacks are initiated when the [Transfer to queue](transfer-to-queue.md) block transfers the initial contact to a callback queue\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/queued-callback-flow-callback-initiation.png)

1. The callback is then placed in the queue\. It remains there until an agent is available and can be offered the contact\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-callback-in-queue.png)

1. When the callback is connected to the agent, a new CTR is created for the contact\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-diagram.png)

1. The **Initiation Timestamp** in the callback CTR corresponds to when the [Transfer to queue](transfer-to-queue.md) block transferred the contact to a callback queue, shown in step 1\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-callback-initiation-timestamp.png)

## How properties in the Transfer to Queue block affect this flow<a name="transfer-to-queue-properties"></a>

The [Transfer to queue](transfer-to-queue.md) block has the following properties, which affect how Amazon Connect handles the callback:
+ **Initial delay**: This property affects when a callback is put in queue\. Specify how much time has to pass between a callback contact being initiated in the contact flow, and the customer being put in queue for the next available agent\. For more information, see [How Initial delay affects Scheduled and In queue metrics](scheduled-vs-inqueue.md)\. 
+ **Maximum number of retries**: If this is set to 2, then Amazon Connect tries to call the customer at most three times: the initial callback, and two retries\. 
+ **Minimum time between attempts**: If the customer doesn't answer the phone, this is how long to wait before trying again\. 