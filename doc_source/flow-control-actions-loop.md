# Loop<a name="flow-control-actions-loop"></a>

When the same action \(the same Action Identifier\) is run multiple times, this block returns a result of "NotDone" a number of times equal to the specified loop count, then "Done" once, then reset\. 

## Parameter object<a name="loop-parameter"></a>

```
{
    "LoopCount": Number of times to loop, must be between 0 and 100 (inclusive). Must either be fully static or fully dynamic.
}
```

## Execution results and conditions<a name="loop-results"></a>

"ContinueLooping" if the loop should continue\. "DoneLooping" if the loop should finish\. Conditions are supported, there must be a Condition provided for Equals ContinueLooping and for Equals DoneLooping, and no other Conditions can be specified\.

## Errors<a name="loop-errors"></a>

None\.

## Restrictions<a name="loop-restrictions"></a>

This is supported in every type of flow\. 

## Corresponding block in the UI<a name="loop-ui"></a>

[Loop](loop.md) 