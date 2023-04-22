# How routing works<a name="about-routing"></a>

Contacts are routed through your contact center based on these factors: 
+ The routing profile an agent is assigned to\.
+ The hours of operation for a given queue\.
+ The routing logic you define in your flows\.

For example, you use routing profiles to route specific types of contacts to agents with specific skill sets\. If no agent with the required skill set is available, you can place the contact in the queue defined in the flow\. 

Here's the logic Amazon Connect uses to route contacts: 
+ Contacts in a queue are automatically prioritized and forwarded to the next available agent \(that is, the agent who has been idle longest\)\.
+ Contacts are placed on hold if there are no available agents\. The order in which they are serviced is determined by their time in queue, on a first\-come, first\-served basis\.
+ If multiple agents are available, the contact is routed to the agent who has been in the **Available** status for the longest time\.
+ A routing profile may assign a priority to one queue over another, but the priority within the queue is always set by the order the contact was added to the queue\.

## How routing works with multiple channels<a name="routing-profile-channels-works"></a>

When you set up a routing profile to handle multiple channels, you must specify whether agents can handle contacts while already on another channel\. This is called cross\-channel concurrency\. 

When using cross\-channel concurrency, Amazon Connect checks which contact to offer the agent as follows: 

1. It checks what contacts/channels the agent is currently handling\.

1. Based on what channels they are currently handling, and the cross\-channel configuration in the agent's routing profile, it determines whether the agent can be routed the next contact\.

For a detailed example of how Amazon Connect routes contacts when cross\-channel concurrency is set up, see [Example of how a contact is routed with cross\-channel concurrency](routing-profiles.md#example-routing-concurrency)\. 

## Learn more about routing<a name="learn-more-about-routing"></a>

See the following topics to learn more about routing:
+ [Concepts: Routing profiles](concepts-routing.md) 
+ [Concepts: Queue\-based routing](concepts-queue-based-routing.md)
+ [Set up queue\-based routing](set-up-queue-based-routing.md) 