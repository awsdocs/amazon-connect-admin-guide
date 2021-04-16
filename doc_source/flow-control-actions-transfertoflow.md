# TransferToFlow<a name="flow-control-actions-transfertoflow"></a>

Execution jumps to a different flow, and continues running at that flow's beginning\. 

## Parameter object<a name="transfertoflow-parameter"></a>

```
{
    "ContactFlowId": A contact flow ID or contact flow ARN. *Must be either fully static or a single valid JSONPath identifier*
}
```

## Execution results and conditions<a name="transfertoflow-results"></a>

None\.

## Errors<a name="transfertoflow-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="transfertoflow-restrictions"></a>

This action is available in inbound flows and transfer flows\. It is not available to hold flows, customer queue flows, or whisper flows\. 

## Corresponding block in the UI<a name="transfertoflow-ui"></a>

[Transfer to flow](transfer-to-flow.md) 