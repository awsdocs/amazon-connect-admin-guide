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

## Queues<a name="concepts-routing-profiles-queues"></a>

There are two types of queues:
+ Standard queues: where the contact waits before they are routed to an agent\.
+ Agent queues: where the contact waits after they’ve been routed to an agent\. Agent queues are created automatically when you add an agent to your contact center\. 

Contacts waiting in agent queues are higher priority than contacts waiting in standard queues\.

## Queues: Priority and Delay<a name="concepts-routing-profiles-priority"></a>

Priority and delay are powerful features that allow you to load balance contacts among groups of agents\. 

For example, one group of agents is assigned to a Sales routing profile\. Since their primary job is sales, the Sales queue is Priority 1 and Delay is 0\. But they can help with Support too, so that queue is Priority 2 and Delay is 0\. This shown in the following table:


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Sales  |  1  |  0  | 
|  Support  |  2  |  0  | 

If there are no calls in the Sales queue, then the agents will be presented with a support call\. 

Say you set Support to Priority 1 and Delay of 30 seconds, as shown in the following table: 


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Sales  |  1  |  0  | 
|  Support  |  1  |  30  | 

These agents will always get sales contacts first, but if a support contact ages past 30 seconds, they will also be presented with the support contact because they are the same priority\. 

Here's a more complicated example for a Support routing profile:


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Tier 1 Support  |  1  |  0  | 
|  Tier 2 Support  |  1  |  0  | 
|  Tier 3 Support  |  2  |  20  | 
|  Tier 4 Support  |  3  |  80  | 

This routing profile prioritizes Tier 1 Support and Tier 2 Support equally because each has a priority 1\.
+ Agents may take contacts for Tier 3 Support when:
  + Customers for Tier 3 Support are waiting for 20 seconds or longer\.
  + And no Tier 1 Support or Tier 2 Support contacts are in queue\.
+ Agents may take contacts for Tier 4 Support when:
  + Customers for Tier 4 Support are waiting 80 seconds or longer\.
  + And no contacts for Tier 1 Support, Tier 2 Support or Tier 3 Support are in queue\.