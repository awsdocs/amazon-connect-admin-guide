# UpdateContactRoutingBehavior<a name="contact-actions-updatecontactroutingbehavior"></a>

Updates the contact's routing details\. This can move the contact forward or backward in queue, specify a queue priority, and set routing attributes\. 

## Parameter object<a name="updatecontactroutingbehavior-parameter"></a>

```
{
    "QueuePriority": An integer that represents the queue priority to be applied to the contact (lower priorities are routed preferentially). Cannot be specified if the QueueTimeAdjustmentSeconds or RoutingProficiencies is specified. Must be statically defined, must be larger than zero, and a valid integer value
    "QueueTimeAdjustmentSeconds": An integer that represents the queue time adjust to be applied to the contact, in seconds (longer / larger queue time are routed preferentially). Cannot be specified if the QueuePriority or RoutingProficiencies is specified. Must be statically defined and a valid integer value
    "RoutingProficiencies": {  An object. Cannot be specified if either QueuePriority or QueueTimeAdjustmentSeconds is specified.
        "AgentHierarchyProficiency": { An object.
            "AgentHierarchy": The ARN of the hierarchy to preferentially route this contact to. Can be dynamic or static, but must be present.
            "ExpirationSeconds": The number of seconds after which to remove this routing proficiency. Can be dynamic or static, but must be present, and if not dynamic must be a valid integer value between 0 and 600 (inclusive).
        }
    }
}
```

## Results and conditions<a name="updatecontactroutingbehavior-results"></a>

None\.

## Errors<a name="updatecontactroutingbehavior-errors"></a>

None\.

## Restrictions<a name="updatecontactroutingbehavior-restrictions"></a>

This is supported only in contact flows\. It is not supported in transfer flows, whisper flows, customer queue flows, or hold flows\. 

## Corresponding block in the UI<a name="updatecontactroutingbehavior-ui"></a>

[Change routing priority / age](change-routing-priority.md)