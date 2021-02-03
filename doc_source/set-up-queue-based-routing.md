# Set up queue\-based \(skills\-based\) routing<a name="set-up-queue-based-routing"></a>

Here's an overview of the steps to set up queue\-based routing:
+ [Create the queues](create-queue.md), for example, one for each skill you want to use for routing\.
+ [Create the routing profiles](routing-profiles.md):
  + Specify the channels supported by this routing profile\.
  + Specify the queues: the channel, priority, and delay\.
+ [Configure agent settings](configure-agents.md) to assign the routing profiles to them\.

When you [create your contact flows](create-contact-flow.md), you'll add the queues to them\. If a contact chooses to speak to an agent in Spanish, for example, they will be routed to the Spanish Reservations queue\. 

For information about how routing works, and queue\-based routing, see these topics:
+ [How routing works with multiple channels](about-routing.md#routing-profile-channels-works)
+ [Queue\-based routing](concepts-queue-based-routing.md)