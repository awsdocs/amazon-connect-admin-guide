# InvokeLambdaFunction<a name="interactions-invokelambdafunction"></a>

Invokes an AWS Lambda function with a collection of optional parameters\. This AWS Lambda function is also given a copy of the flow run data if there is an associated contact with the flow\. 

## Parameter object<a name="invokelambdafunction-parameter"></a>

```
{
    "LambdaFunctionARN": The ARN of the AWS Lambda function to be invoked. May be defined statically or dynamically. 
    "InvocationTimeLimitSeconds": The number of seconds to wait for a response from the AWS Lambda function. Must be greater than 0, no larger than 8, and an integer. Must be set statically. 
    "LambdaInvocationAttributes" { A map of additional data to send to the AWS Lambda function when invoking it. Keys and values may be set statically or dynamically.
    }
}
```

## Results and conditions<a name="invokelambdafunction-results"></a>

None\. Conditions are not supported\. If an error does not occur, the response's attributes are available dynamically under the $\.External path\. 

## Errors<a name="invokelambdafunction-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="invokelambdafunction-restrictions"></a>

None\. This action is supported by all channels and in all types of flows\.

## Corresponding block in the UI<a name="invokelambdafunction-ui"></a>

[Invoke AWS Lambda function](invoke-lambda-function-block.md)