# Routing Profiles<a name="concepts-routing"></a>

A routing profile determines what types of contacts an agent can receive and the routing priority\. 
+ Each agent is assigned to one routing profile\.
+ A routing profile can have multiple agents assigned to it\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agents-routing-profile.png)

Amazon Connect uses routing profiles to allow you to manage your contact center at scale\. To quickly change what a group of agents does, you only need to make an update in one place: the routing profile\.

## Routing Profiles Link Queues and Agents<a name="concepts-routing-profiles-queues"></a>

When you create a routing profile, you specify: 
+ The channels the agents will support\.
+ The queues of customers that the agents will handle\. You can use a single queue to handle all incoming contacts, or you can set up multiple queues\. Queues are linked to agents through a routing profile\.
+ Priority and delay of the queues\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/routing-profile-3.png)