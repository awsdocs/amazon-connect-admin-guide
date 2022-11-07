# UpdateContactTargetQueue<a name="contact-actions-updatecontacttargetqueue"></a>

Sets the contact's TargetQueue\. This is the queue is used by all other instructions that check a queue implicitly, and for TransferContactToQueue\. 

## Parameter object<a name="updatecontacttargetqueue-parameter"></a>

```
{
  "QueueId": [Optional] A queue ID or queue ARN. If AgentId is specified, this may not be specified. This must be either defined fully statically or as a single valid JSONPath identifier.
  "AgentId": [Optional] An agent ID or agent ARN, representing an agent queue. If QueueId is specified, this may not be specified. This must be either defined fully statically or as a single valid JSONPath identifier.
}
```

## Results and conditions<a name="updatecontacttargetqueue-results"></a>

None\.

## Errors<a name="updatecontacttargetqueue-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="updatecontacttargetqueue-restrictions"></a>

This action is supported only in inbound contact flows and transfer flows\. It is not supported in whisper flows, hold flows, or customer queue flows\. 

## Corresponding block in the UI<a name="updatecontacttargetqueue-ui"></a>

[Set customer queue flow](set-customer-queue-flow.md)