# UpdateFlowLoggingBehavior<a name="flow-control-actions-updateflowloggingbehavior"></a>

Enables or disables flow logging\. If this is a flow, this same behavior remains unless it is overridden for the rest of the contact segment\. It is also automatically inherited by new segments in the chain\. 

## Parameter object<a name="updateflowloggingbehavior-parameter"></a>

```
{ 
  "FlowLoggingBehavior": One of [Enabled,Disabled]. *Dynamic values are not supported*
}
```

## Results and conditions<a name="updateflowloggingbehavior-results"></a>

None\. No conditions are supported\.

## Errors<a name="updateflowloggingbehavior-errors"></a>

None\.

## Restrictions<a name="updateflowloggingbehavior-restrictions"></a>

This action is available in every type of flow\. 

## Corresponding block in the UI<a name="updateflowloggingbehavior-ui"></a>

[Set logging behavior](set-logging-behavior.md) 