# Actions in the Amazon Connect Flow Language<a name="flow-language-actions"></a>

An Action is a single step of a flow's run\. This topic describes the fields that must be defined\.

## Identifier<a name="flow-language-actions-identifier"></a>

A string that must be unique among all Actions within the same Flow\. This Identifier can be up to 50 characters long, and can include any characters \(including unicode and spaces\)\. They can be opaque or user\-friendly\.

## Type<a name="flow-language-actions-type"></a>

A string that identifies the type of action being performed for a particular step of the Flow\. This type must be one of a list of allowable Types, which are covered later\.

## Parameters<a name="flow-language-actions-parameters"></a>

An object that defines the customizable behavior of a particular Action block\. Each Action has its own format of this Parameters object, which is detailed in the individual Actions definition\.

The Parameters object defines customizable behavior for the Action\. For example, it defines which Attributes to set or which AWS Lambda function to run\. The format differs for each Action type\. To find the specific format of a specific Action's Parameter object, see the individual Action's definition below\.

## Transitions<a name="flow-language-actions-transitions"></a>

An object that defines the behavior for choosing the next Action after the current Action completes\. Certain Actions terminate, meaning that they finish running the flow when they're run\. This is because Transitions must be defined as an empty object\.

The Transitions object defines how to proceed to the next Action during flow runtime\. This object must have the following fields specified:

### NextAction<a name="flow-language-actions-transitions-nextaction"></a>

NextAction is a string that contains the Identifier of the Action that should be run after this Action, if no error or condition is preferentially chosen\.

### Errors<a name="flow-language-actions-transitions-errors"></a>

Errors is a list of error objects\. Each error object contains a type or category of error \(ErrorType\), and the Identifier of the Action that should be run subsequently when that error occurs \(NextAction\)\. 

Each individual Action supports specific Errors, detailed in the Action's definition later, and the following commonly supported errors:
+ NoMatchingError\. This is invoked when an error occurs and no other Error matches\.
+ NoMatchingCondition\. This is invoked if no defined condition resolves to true\.

### Conditions<a name="flow-language-actions-transitions-conditions"></a>

Conditions are an ordered list that defines a series of checks to evaluate against the Action's result\. This result changes per Action and can also change based on Parameters \- examples of these are "the number of contacts in queue" for the CheckMetricData Action if the MetricType parameter refers to the NumberOfContactsInQueue, and "the value of the attribute" for the Compare Action\. Conditions are evaluated in order, and the first Condition that evaluates to true will result in it being chosen as the Transition to occur, making that Condition's Target the next Action run\. The Conditions object is explained in more detail below\.

A Condition is a definition of how to evaluate an Action's result, and may evaluate to true or false\. The Conditions object on the flow contains an ordered list of objects\. Each object contains a NextAction \(the Identifier of the Action to be invoked if the Condition evaluates to be true\) and the Condition to evaluate:
+ NextAction: A string that contains the Identifier of the Action that should be run after this Action if this Condition is the first condition to evaluate to true\.
+ Condition: An object that defines the evaluation logic\.

#### The Condition object<a name="flow-language-actions-transitions-condition-object"></a>

The Condition object must contain the following fields:
+ **Operator**: A string that indicates which comparison operator that is applied to the Operands\. The list of allowed Operators and a description of their logic is defined in the following table\.
+ **Operands**: A list of operands to which the Operator is applied\. Depending on the Operator, these Operands may be strings or they may be Condition objects\. The specific Operator defines which type of Operand is expected, along with the number of Operands expected \(some Operators will require only one Operand, some will support a list of up to ten Operands\)\. Conditions may be nested no more than five Conditions deep, and a single Condition may not contain more than 50 sub\-Conditions, regardless of how deeply nested they are\.

## List of Operators<a name="flow-language-actions-operators"></a>


| Operator | Description | Operand type | Operand count | 
| --- | --- | --- | --- | 
|  Equals  | Returns **true** if the string specified exactly equals the result\.  | String | One | 
|  TextStartsWith  | Returns **true** if the result, interpreted as text, begins with the specified string\.  | String | One | 
|  TextEndsWith  | Returns **true** if the result, interpreted as text, ends with the specified string\.  | String | One | 
|  TextContains  | Returns **true** if the result, interpreted as text, contains the specified string at least once\.  | String | One | 
|  NumberGreaterThan  | Returns **true** if the result, interpreted as a numeric value, is larger than the specified string\. If either the result or the specified string are not numeric, returns **false**\.  | String | One | 
|  NumberGreaterOrEqualTo  | Returns **true** if the result, interpreted as a numeric value, is larger than or equal to the specified string\. If either the result or the specified string are not numeric, returns **false**\.  | String | One | 
|  NumberLessThan  | Returns **true** if the result, interpreted as a numeric value, is smaller than the specified string\. If either the result or the specified string are not numeric, returns **false**\.  | String | One | 
|  NumberLessOrEqualTo  | Returns **true** if the result, interpreted as a numeric value, is smaller than or equal to the specified string\. If either the result or the specified string are not numeric, returns **false**\.  | String | One | 

### Example Condition<a name="flow-language-actions-example-condition"></a>

Following is an example of a condition that returns true if the result starts with "ABC":

```
{
    "Operator": "TextStartsWith",
    "Operands": [
        "ABC"
    ]
}
```