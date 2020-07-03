# Create a routing profile<a name="routing-profiles"></a>

While queues are a 'waiting area' for contacts, a routing profile links queues to agents\. When you create a routing profile, you specify which queues will be in it\. You can also specify whether one queue should be prioritized over another\. 

Each agent is assigned to one routing profile\. 

**To create a routing profile**

1. Choose **Users**, **Routing profiles**, **Add new profile**\.

1. Enter or choose the following information:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles.html)

1. Under **Routing profile queues**, enter the following information:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles.html)

1. Choose **Add new profile**\.

## Tips for setting up channels and concurrency<a name="routing-profile-concurrency"></a>
+ Use **Set channels and concurrency** to toggle on and off whether agents assigned to a profile get voice and chat contacts\. 

  For example, there are 20 queues assigned to a profile\. All of the queues are enabled for both voice and chat\. By removing the **Voice** option at the routing profile level, you can stop all voice calls to these agents, across all queues in the profile\. When you want to restart voice contacts for these agents again, select **Voice**\. 
+ For each queue in the profile, choose whether it's for voice or chat contacts, or both\. 
+ If you want a queue to handle both voice and chat contacts, but want to assign a different priority to each channel, add the queue twice, like this:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-queue.png)