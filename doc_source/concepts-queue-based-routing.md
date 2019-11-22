# Queue\-Based Routing<a name="concepts-queue-based-routing"></a>

In your business, you might want to route customers to specific agents based on certain criteria, such as the skill of the agent\. This is called queue\-based routing, also known as skills\-based routing\. 

For example, an airline might have some agents who handle reservations for English\-speaking customers, others who handle Spanish\-speaking customers, and a third group who handle both types of customers, but only over the phone\.

The following illustration shows you can: 
+ Assign the same routing profile to multiple agents\.
+ Assign multiple queues to a routing profile\.
+ Assign a queue to multiple routing profiles\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-example2.png)

To set up queue\-based routing:
+ [Create the queues](create-queue.md), for example, one for each skill you want to use for routing\.
+ [Create the routing profiles](routing-profiles.md):
  + Specify the channels supported by this routing profile\.
  + Specify the queues: the channel, priority, and delay\.
+ [Configure agent settings](configure-agents.md) to assign the routing profiles to them\.

When you build your contact flows, you'll add the queues to them\. If a contact chooses to speak to an agent in Spanish, for example, they will get routed to the Spanish Reservations queue\. 