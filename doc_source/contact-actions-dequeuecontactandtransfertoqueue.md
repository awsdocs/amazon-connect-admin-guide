# DequeueContactAndTransferToQueue<a name="contact-actions-dequeuecontactandtransfertoqueue"></a>

This action is a combination of a "Dequeue" action and a "TransferContactToQueue" action\. This means that a contact in a queue is removed from the queue, a new contact segment is created with the existing contact as its previous contact, and the new contact is placed into the specified queue \(referred to as "Queue\-to\-queue transfer"\)\. If this contact has not been queued, is actively being joined to an agent, or has been routed to an agent, this action fails\. 

## Parameter object<a name="dequeuecontactandtransfertoqueue-parameter"></a>

```
{
    "QueueId": [Optional] A queue ID or queue ARN. If AgentId is specified, this may not be specified. Must be either fully statically defined or a single, valid JSONPath identifier.
    "AgentId": [Optional] An agent ID or agent ARN, representing an agent queue. If QueueId is specified, this may not be specified. Must be either fully statically defined or a single, valid JSONPath identifier.
}
```

## Results and conditions<a name="dequeuecontactandtransfertoqueue-results"></a>

None\.

## Errors<a name="dequeuecontactandtransfertoqueue-errors"></a>
+ QueueAtCapacity \- if the destination queue is at capacity and the contact cannot be queued within it\.
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="dequeuecontactandtransfertoqueue-restrictions"></a>

This action is only supported in the customer queue flow\. It is not supported in any other type of flow\. 

## Corresponding block in the UI<a name="dequeuecontactandtransfertoqueue-ui"></a>

Maps to [Transfer to flow](transfer-to-flow.md) but only when used in a Customer queue flow\.