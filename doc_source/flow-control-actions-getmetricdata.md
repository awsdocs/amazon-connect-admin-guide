# GetMetricData<a name="flow-control-actions-getmetricdata"></a>

Loads real time queue metrics for the queue specified by queue ID, agent ID \(for agent queues\), or the target queue, and makes them available on the flow run data\. May be extended in the future to allow getting historical metric data in addition to current metric data, and to getting agent metrics in addition to queue metrics\. 

## Parameter object<a name="getmetricdata-parameter"></a>

```
{ 
  "QueueId": [Optional] A queue ID or queue ARN. If AgentId is specified, this may not be specified. *Dynamic values are supported*,
  "AgentId": [Optional] An agent ID or agent ARN, representing an agent queue. If QueueId is specified, this may not be specified. *Dynamic values are supported*
  "QueueChannel": [Optional] Either "Voice" or "Chat". Can be set dynamically. Determines the channel for which metrics are returned. If not specified, metrics are returned for all channels.
}
```

## Execution results and conditions<a name="getmetricdata-results"></a>

None\. No conditions are supported\.

## Errors<a name="getmetricdata-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="getmetricdata-restrictions"></a>

This action is available in every type of flow\. 

## Corresponding block in the UI<a name="getmetricdata-ui"></a>

[Get queue metrics](get-queue-metrics.md) 