# CompleteOutboundCall<a name="contact-actions-completeoutboundcall"></a>

When a flow is run before an outbound call is made as part of an outbound contact, this action calls the outbound destination\. If this action is not used, the first participant action implicitly completes the outbound call\. 

## Parameter object<a name="completeoutboundcall-parameter"></a>

```
{
    "CallerId": { Optional, an override of the caller ID to present when calling
        "Number": The caller ID number to present when calling. Can either be fully static or a single valid JSONPath identifier
        "Name": The caller ID name to present when calling. **This is not currently supported on the UI, so it should be treated as unknown but is an area of expansion since we should support name anywhere we support number ideally**
    }
}
```

## Results and conditions<a name="completeoutboundcall-results"></a>

None\.

## Errors<a name="completeoutboundcall-errors"></a>

None\.

## Restrictions<a name="completeoutboundcall-restrictions"></a>

This action can be used only when the contact is in the process of making an outbound call, but has not yet called the outbound number\. 

## Corresponding block in the UI<a name="completeoutboundcall-ui"></a>

[Call phone number](call-phone-number.md) 