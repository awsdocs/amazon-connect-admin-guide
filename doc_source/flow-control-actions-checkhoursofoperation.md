# CheckHoursOfOperation<a name="flow-control-actions-checkhoursofoperation"></a>

Returns whether the specified hours of operation object \(or the hours of operation object associated with the current queue if no hours of operation is referenced\) is in hours or out of hours as its result, allowing comparisons against it\. 

## Parameter object<a name="checkhoursofoperation-parameter"></a>

```
{ 
  "HoursOfOperationId": [Optional] An hours of operation ID or hours of operation ARN. *Must be either fully static or fully dynamic*. If not specified, the TargetQueue's hours of operation for the contact are used
}
```

## Results and conditions<a name="checkhoursofoperation-results"></a>

**True** or **False** based on whether the hours of operation object specified is in hours or out of hours\. There must be a Condition provided for Equals **True** and a Condition for Equals **False**, and no other conditions\.

## Errors<a name="checkhoursofoperation-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="checkhoursofoperation-restrictions"></a>

This action is available in inbound flows, transfer flows, and customer queue flows\. It is not available to hold flows or to whisper flows\. 

## Corresponding block in the UI<a name="checkhoursofoperation-ui"></a>

[Check hours of operation](check-hours-of-operation.md) 