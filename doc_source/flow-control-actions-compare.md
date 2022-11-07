# Compare<a name="flow-control-actions-compare"></a>

Allows comparisons against the specified value\. 

## Parameter object<a name="ompare-parameter"></a>

```
{
  "ComparisonValue": Any **single** JSONPath identifier that is valid for the flow data object
}
```

## Execution results and conditions<a name="fcompare-results"></a>

The value specified for comparison\. This can be used for conditions\.

## Errors<a name="compare-errors"></a>
+ NoMatchingCondition \- if no other Condition matches\. 

## Restrictions<a name="compare-restrictions"></a>

This action is available in every type of flow\. 

## Corresponding block in the UI<a name="compare-ui"></a>

[Check contact attributes](check-contact-attributes.md) 