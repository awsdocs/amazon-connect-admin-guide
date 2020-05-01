# Queues: Priority and Delay<a name="concepts-routing-profiles-priority"></a>

Priority and delay are powerful features that allow you to load balance contacts among groups of agents\. 

## Example 1: Different priority but same delay<a name="concepts-routing-profiles-priority-example1"></a>

For example, one group of agents is assigned to a Sales routing profile\. Since their primary job is sales, the Sales queue is Priority 1 and Delay is 0\. But they can help with Support too, so that queue is Priority 2 and Delay is 0\. This shown in the following table:


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Sales  |  1  |  0  | 
|  Support  |  2  |  0  | 

If there are no contacts in the Sales queue, then the agents will be presented with contacts from the Support queue\. 

## Example 2: Same priority but different delay<a name="concepts-routing-profiles-priority-example2"></a>

Say you set the Support queue to Priority 1 and Delay of 30 seconds, as shown in the following table: 


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Sales  |  1  |  0  | 
|  Support  |  1  |  30  | 

These agents will always get contacts from the Sales queue first because the delay is 0\. However, when a contact in the **Support** queue ages past 30 seconds, it will also be treated as priority 1\. The agents will then be presented with the contact from the **Support** queue\. 

## Example 3: Different Priorities and Delays<a name="concepts-routing-profiles-priority-example3"></a>

Here's a more complicated example for a Support routing profile:


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Tier 1 Support  |  1  |  0  | 
|  Tier 2 Support  |  1  |  0  | 
|  Tier 3 Support  |  2  |  20  | 
|  Tier 4 Support  |  3  |  80  | 

This routing profile prioritizes the Tier 1 Support and Tier 2 Support queues equally because each is priority 1\.
+ Agents may take contacts from the Tier 3 Support queue when:
  + Customers for Tier 3 Support are waiting for 20 seconds or longer\.
  + And no contacts are in the Tier 1 Support or Tier 2 Support queues\.
+ Agents may take contacts from the Tier 4 Support queue when:
  + Customers in the Tier 4 Support queue have been waiting 80 seconds or longer\.
  + And no contacts are in the Tier 1 Support, Tier 2 Support or Tier 3 Support queues\.

## Example 4: Same Priority and Delay<a name="concepts-routing-profiles-priority-example4"></a>

In this example a routing profile has only two queues, and they have the same priority and delay:


| Queue | Priority | Delay \(in seconds\) | 
| --- | --- | --- | 
|  Sales  |  1  |  0  | 
|  Support  |  1  |  0  | 

For this routing profile, the oldest contact is routed to an agent first, regardless of queue\. 