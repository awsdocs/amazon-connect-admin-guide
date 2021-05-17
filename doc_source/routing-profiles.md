# Create a routing profile<a name="routing-profiles"></a>

While queues are a 'waiting area' for contacts, a routing profile links queues to agents\. When you create a routing profile, you specify which queues will be in it\. You can also specify whether one queue should be prioritized over another\. 

Each agent is assigned to one routing profile\. For more information about routing profiles and queues, see [Routing profiles](concepts-routing.md)\.

**To create a routing profile**

1. On the navigation menu, choose **Users**, **Routing profiles**, **Add new profile**\.

1. Enter or choose the following information:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles.html)

1. Under **Routing profile queues**, enter the following information:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles.html)

1. Choose **Add new profile**\.

## Tips for setting up channels and concurrency<a name="routing-profile-concurrency"></a>
+ Use **Set channels and concurrency** to toggle on and off whether agents assigned to a profile get voice, chat, and task contacts\. 

  For example, there are 20 queues assigned to a profile\. All of the queues are enabled for voice, chat, and task\. By removing the **Voice** option at the routing profile level, you can stop all voice calls to these agents, across all queues in the profile\. When you want to restart voice contacts for these agents again, select **Voice**\. 
+ For each queue in the profile, choose whether it's for voice, chat, task, or all three\. 
+ If you want a queue to handle voice, chat, and task, but want to assign a different priority to each channel, add the queue twice\. For example, in the following image, voice is priority 1 but chat and task are priority 2\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-channels-and-concurrency-2.png)

## Delete a routing profile<a name="delete-routing-profiles"></a>

Currently it's not possible to delete a routing profile\. To take a routing profile out of use, detach it from the agents\.

To indicate that the routing profile is no longer in use, we recommend renaming it with a **zz\_** prefix, for example, zz\_Sales\.