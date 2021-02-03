# CreateCallbackContact<a name="interactions-createcallbackcontact"></a>

Creates a new callback contact\. If no customer number is specified, and this is run in context of a contact, the contact's CustomerCallbackNumber is used as the customer number\. 

## Parameter object<a name="createcallbackcontact-parameter"></a>

```
{
    "QueueId": [Optional] A queue ID or queue ARN. The callback contact is routed with this queue, or if this is not specified, the contact's current TargetQueue. Must be specified fully statically or with a single valid JSONPath identifier.
    "AgentId": [Optional] An agent ID or agent ARN, representing an agent queue. If QueueId is specified, this may not be specified. This must be either defined fully statically or as a single valid JSONPath identifier.
    "InitialCallDelaySeconds": The amount of time, in seconds, to wait at a minimum before routing the callback contact. This gives the customer enough time to end their existing contact before being called back. Must be larger than 0, no greater than 259,200 (three days), and an integer. Must be defined statically.
    "MaximumConnectionAttempts": The number of attempts at a maximum to connect this contact to a customer, if the callback is not answered. Must be larger than zero, and an integer. Must be defined statically.
    "RetryDelaySeconds": The minimum amount of time to wait, in seconds, between an unanswered callback attempt is made and the next attempt to reach the customer. Must be larger than 0, no greater than 259,200 (three days), and an integer. Must be defined statically.
}
```

## Results and conditions<a name="createcallbackcontact-results"></a>

None\. No conditions are supported\. 

## Errors<a name="createcallbackcontact-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="createcallbackcontact-restrictions"></a>

This action is supported in contact flows, transfer flows, and customer queue flows\. It is not supported in whisper flows or hold flows\.

## Corresponding block in the UI<a name="createcallbackcontact-ui"></a>

[Set callback number](set-callback-number.md)