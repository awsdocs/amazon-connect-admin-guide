# CheckMetricData<a name="flow-control-actions-checkmetricdata"></a>

A shortcut single action to avoid using GetMetricData and Compare for a set of simple metrics\. This action loads the specified metric data for the specified queue, and allows comparisons to the loaded value\. For example, it loads number of contacts in queue, age of oldest contact in queue, number of agents staffed on the queue, number of agents available on the queue, or number of agents online on the queue\. 

## Parameter object<a name="checkmetricdata-parameter"></a>

```
{
  "MetricType": One of [NumberOfAgentsAvailable, NumberOfAgentsStaffed, NumberOfAgentsOnline, OldestContactInQueueAgeSeconds, NumberOfContactsInQueue]. **Dynamic values are not supported**,
  "QueueId": [Optional] A queue ID or queue ARN. If AgentId is specified, this may not be specified. *Dynamic values are supported*,
  "AgentId": [Optional] An agent ID or agent ARN, representing an agent queue. If QueueId is specified, this may not be specified. *Dynamic values are supported*. If neither this nor QueueId are specified, the contact TargetQueue is used
}
```

## Execution results and conditions<a name="checkmetricdata-results"></a>

A number, representing the value of the metric that was requested\. This can be used for conditions\. If the MetricType is NumberOfAgents\* then the only supported condition is "NumberGreaterThan 0", otherwise Equals and any Number\* Operands are allowed\.

## Errors<a name="checkmetricdata-errors"></a>
+ NoMatchingError \- if no other Error matches\.
+ NoMatchingCondition \- if no other Condition matches \(only supported if the MetricType is OldestContactInQueueAgeSeconds or NumberOfContactsInQueue\)\.

## Restrictions<a name="checkmetricdata-restrictions"></a>

This action is only usable in contact flows, queue and agent transfers, and customer queue flows\. It is not available in any type of whisper or hold flows\. 

## Corresponding block in the UI<a name="compare-ui"></a>

None\.