# EndFlowExecution<a name="flow-control-actions-endflowexecution"></a>

Finishes flow, but does not explicitly disconnect the participant\. The participant may be disconnected by contact logic after this\. For example, if a contact flow ends before the contact is put into queue, ending the flow results in the contact being ended\. 

## Parameter object<a name="endflowexecution-parameter"></a>

```
{
   
}
```

## Results and conditions<a name="endflowexecution-results"></a>

None\. No conditions are supported\.

## Errors<a name="endflowexecution-errors"></a>

None\. This is always a terminal action\.

## Restrictions<a name="endflowexecution-restrictions"></a>

This action is available only in whisper flows and customer queue flows\. It is not available in contact flows, hold flows, or transfer flows\. 

## Corresponding block in the UI<a name="endflowexecution-ui"></a>

[End flow / Resume](end-flow-resume.md) 