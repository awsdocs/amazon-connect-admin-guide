# Create a routing profile<a name="routing-profiles"></a>

While queues are a 'waiting area' for contacts, a routing profile links queues to agents\. When you create a routing profile, you specify: 
+ Channels: Which channels—voice, chat, task—are routed to this group of agents; whether to allow channels concurrently\.
+ Queues: Which queues are in the routing profile; whether one queue should be prioritized over another\.

Each agent is assigned to one routing profile\. For more information about routing profiles and queues, see [Concepts: Routing profiles](concepts-routing.md)\.

**How many routing profiles can I create?** To view your quota of **Routing profiles per instance**, open the Service Quotas console at [https://console\.aws\.amazon\.com/servicequotas/](https://console.aws.amazon.com/servicequotas/)\.

**To create a routing profile**

1. On the navigation menu, choose **Users**, **Routing profiles**, **Add routing profile**\.

1. In the **Routing Profile Details** section, in the **Name** box, enter a searchable display name\. In the **Description** box, enter what the profile is used for\. 

1. In the **Channel Settings** section, enter or choose the following information:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles.html)

1. In the **Queues** section, enter the following information:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles.html)

1. In the **Tags** section, add [tags](tagging.md) to manage who can access routing profiles\.

1. Choose **Save**\.

## Tips for setting up channels and concurrency<a name="routing-profile-concurrency"></a>
+ Use **Channel availability** to toggle on and off whether agents assigned to a profile get voice, chat, and task contacts\. 

  For example, there are 20 queues assigned to a profile\. All of the queues are enabled for voice, chat, and task\. By removing the **Voice** option at the routing profile level, you can stop all voice calls to these agents, across all queues in the profile\. When you want to restart voice contacts for these agents again, select **Voice**\. 
+ When using **Cross\-channel concurrency**, Amazon Connect checks which contact to offer the agent as follows: 

  1. It checks what contacts/channels the agent is currently handling\.

  1. Based on what channels they are currently handling, and the cross\-channel configuration in the agent's routing profile, it determines whether the agent can be routed the next contact\.

  1. Amazon Connect prioritizes the longest waiting contact if Priority and Delay are equal\. Even though it's evaluating multiple channels at the same time, First\-In First\-Out is still respected\.

  See [Example of how a contact is routed with cross\-channel concurrency](#example-routing-concurrency)\.
+ For each queue in the profile, choose whether it's for voice, chat, task, or all three\. 
+ If you want a queue to handle voice, chat, and task, but want to assign a different priority to each channel, add the queue twice\. For example, in the following image, voice is priority 1 but chat and task are priority 2\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-channels-and-concurrency-2.png)

## Example of how a contact is routed with cross\-channel concurrency<a name="example-routing-concurrency"></a>

For example, assume an agent is assigned to the routing profile that has the channel settings shown in the following image\. They can be routed voice, chat, and task contacts\. They can receive cross\-channel contacts when on tasks\. 

![\[The create routing profile page, channel settings section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-cross-channel-concurrency.png)

The agent will experience the following routing behavior:

1. Assume the agent is fully idle\. Next, the agent accepts a chat and begins working on it\. Meanwhile, a task comes into queue\.
   + Chat is set to **No other channels allowed**\. 
   + So even though there is a task in queue, it will not be offered to this agent\.

1. Next, there is a chat in queue\.
   + The agent's maximum chat concurrency is 2, so they are routed another chat for total of 2 chats\. The agent continues working on both of the chats\.

1. There are no other chats in queue\. The agent finishes both chats \(closes ACW\)\. 
   + There is still a task waiting in queue\.
   + At this point, the task is offered to the agent because they are fully idle again\. The agent begins working the task\.

1. Another chat comes into queue\.
   + Tasks is set to **Allow other channels concurrently**\. So, even though the agent is already working on a task, they can still be offered the chat\. 
   + The chat gets routed to the agent, who now works on both the 1 chat and 1 task concurrently\.

1. Now there is a Voice call in queue\.
   + The agent is still working on 1 chat and 1 task\. 
   + Even though **Task** is set to **Allow other channels concurrently**, the agent is still working on 1 chat, and **Chat** is set to **No other channels while agent is on a Chat contact**\. So, the voice call is not routed to the agent\. The agent continues working on both the chat and the task\.

1. The agent completes the chat, but still works on the task\.
   + Now, because the only contact still assigned to the agent is a task, and **Tasks** are set to **Allow other channels concurrently**, this means that the agent can be offered the voice call\. 
   + The agent picks up the voice call and is now working concurrently on both the voice call and the task\. 

1. Now there is another task in queue\.
   + The agent is currently working on a voice call AND a task\. Once again, Amazon Connect checks the cross channel settings and Voice is set to **No other channels while agent is on a Voice contact**\. 
   + Because the agent is working on a voice call, they cannot be offered any tasks until they are done with the voice call\. 
   + Also, because **Task** is set to **Maximum contacts per agent** is 1, even after the agent handles the voice call, they still won't be offered the task until they finish their current task\. 

## Delete a routing profile<a name="delete-routing-profiles"></a>

Currently it's not possible to delete a routing profile\. To take a routing profile out of use, detach it from the agents\.

To indicate that the routing profile is no longer in use, we recommend renaming it with a **zz\_** prefix, for example, zz\_Sales\.