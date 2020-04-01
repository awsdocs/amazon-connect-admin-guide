# Queues: Priority and Delay<a name="concepts-routing-profiles-priority"></a>

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

These agents will always get sales contacts first, but if a sales contact ages past 30 seconds, they will also be presented with the support contact because they are the same priority\. 

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