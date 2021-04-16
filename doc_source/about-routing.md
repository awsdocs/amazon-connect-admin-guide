# How routing works<a name="about-routing"></a>

Contacts are routed through your contact center based on these factors: 
+ The routing profile an agent is assigned to\.
+ The hours of operation for a given queue\.
+ The routing logic you define in your contact flows\.

For example, you use routing profiles to route specific types of contacts to agents with specific skill sets\. If no agent with the required skill set is available, you can place the contact in the queue defined in the contact flow\. 

Here's the logic Amazon Connect uses to route contacts: 
+ Contacts in a queue are automatically prioritized and forwarded to the next available agent\.
+ Contacts are placed on hold if there are no available agents\. The order in which they are serviced is determined by their time in queue, on a first\-come, first\-served basis\.
+ If multiple agents are available, the contact is routed to the agent who has been in the **Available** status for the longest time\.
+ A routing profile may assign a priority to one queue over another, but the priority within the queue is always set by the order the contact was added to the queue\.

## How routing works with multiple channels<a name="routing-profile-channels-works"></a>

When you set up a routing profile to handle multiple channels, agents must complete the interactions with inbound contacts on one channel before they can receive a contact or a task on the other\. 

**Example**: Say a routing profile is configured for voice contacts and for up to 5 chats and up to 10 tasks\. Here's how it would work: 
+ When agents sign on, they can be routed a chat, task, or voice contact\.
+ After the agents begin interacting with a voice call, no chats, tasks, or additional voice contacts are routed to them until they finish the call\. 
+ When agents accept a chat, up to 5 chats are routed to them, but no voice contacts or tasks\. After they're done with the chats, they're available for the next contact, which could be voice, chat, or task\. 
+ When agents accept a task, up to 10 tasks are routed to them, but no voice contacts or chats\. After they're done with the tasks, they're available for the next contact, which could be voice, chat, or task\. 

This routing model allows agents to handle both voice and chat channels\. It routes contacts to the agent based on the type of contact the agent is already on\. This way, if an agent is already chatting with a customer, it's more efficient for the agent to respond to more chats instead of multitasking on two different channels\.

To learn how to set up multiple channels, see [Create a routing profile](routing-profiles.md)\.

## Learn more about routing<a name="learn-more-about-routing"></a>

See the following topics to learn more about routing:
+ [Routing profiles](concepts-routing.md) 
+ [Queue\-based routing](concepts-queue-based-routing.md)
+ [Set up queue\-based routing](set-up-queue-based-routing.md) 