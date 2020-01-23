# How Initial Delay Affects Scheduled and In Queue Metrics<a name="scheduled-vs-inqueue"></a>

In the [Transfer to queue](transfer-to-queue.md) block, the **Initial delay** property affects when a callback is put in queue\. For example, assume **Initial delay** is set to 30 seconds\. Here's what appears in your real\-time metrics report:

1. After 20 seconds, the callback has already been created, but it is not yet in queue because of the **Initial delay** setting\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-callback-scheduled.png)

1. After 35 seconds, the callback contact has been placed in queue\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-callback-in-queue2.png)

1. Assume that after 40 seconds, an agent accepts the callback\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-callback-accepted-by-agent.png)