# Invoke AWS Lambda functions<a name="connect-lambda-functions"></a>

Amazon Connect can interact with your own systems and take different paths in contact flows dynamically\. To achieve this, invoke AWS Lambda functions in a contact flow, fetch the results, and call your own services or interact with other AWS data stores or services\. For more information, see the [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/)\.

To invoke a Lambda function from a contact flow, complete the following tasks\.

**Topics**
+ [Create a Lambda function](#create-lambda-function)
+ [Add a Lambda function to your Amazon Connect instance](#add-lambda-function)
+ [Invoke a Lambda Function from a Contact Flow](#function-contact-flow)
+ [Configure your Lambda function to parse the event](#function-parsing)
+ [Verify the function response](#verify-function)
+ [Consume the Lambda function response](#process-function-response)

## Create a Lambda function<a name="create-lambda-function"></a>

Create a Lambda function, using any runtime, and configure it\. For more information, see [Create a Lambda Function](https://docs.aws.amazon.com/lambda/latest/dg/get-started-create-function.html) in the *AWS Lambda Developer Guide*\.

If you create the Lambda function in the same Region as your contact center, you can use the Amazon Connect console to add the Lambda function to your instance as described in the next task, [Add a Lambda function to your Amazon Connect instance](#add-lambda-function)\. This automatically adds resource permissions that allow Amazon Connect to invoke the Lambda function\. Otherwise, if the Lambda function is in a different Region, you can add it to your contact flow using the contact flow designer and add the resource permissions using the [add\-permission](https://docs.aws.amazon.com/cli/latest/reference/lambda/add-permission.html) command, with a principal of `connect.amazonaws.com` and the ARN of your Amazon Connect instance\. For more information, see [Using Resource\-Based Policies for AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html) in the *AWS Lambda Developer Guide*\.

## Add a Lambda function to your Amazon Connect instance<a name="add-lambda-function"></a>

Before you can use an Lambda function in a contact flow, you need to add it to your Amazon Connect instance\.

**Add a Lambda function to your instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the name of the instance from the **Instance Alias** column\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot18.png)

1. In the navigation pane, choose **Contact flows**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot19.png)

1. In the **AWS Lambda** section, use the **Function** drop\-down box to select the function to add to your instance\.
**Tip**  
The drop\-down lists only those functions in the same Region as your instance\. If no functions are listed, choose **Create a new Lambda function**, which opens the AWS Lambda console\.  
To use a Lambda in a different Region or account, in the [Invoke AWS Lambda function](invoke-lambda-function-block.md), under **Select a function**, you can enter the ARN of a Lambda\. Then set up the corresponding resource\-based policy on that Lambda to allow the contact flow to call it\.   
To call `lambda:AddPermission`, you need to:  
Set the principal to **connect\.amazonaws\.com**
Set the source account to be the account your instance is in\.
Set the source ARN to the ARN of your instance\.
For more information, see [Granting function access to other accounts](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html#permissions-resource-xaccountinvoke)\.

1. Choose **Add Lambda Function**\. Confirm that the ARN of the function is added under **Lambda Functions**\.

Now you can refer to that Lambda function in your contact flows\.

## Invoke a Lambda Function from a Contact Flow<a name="function-contact-flow"></a>

To view a contact flow that invokes a Lambda function, see [Sample Lambda integration](sample-lambda-integration.md)\.

1. Open or create a contact flow\.

1. Add an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block \(in the **Integrate** group\) to the grid\. Connect the branches to and from the block\.

1. Choose the title of the [Invoke AWS Lambda function](invoke-lambda-function-block.md) block to open its properties page\.

1. Under **Select a function**, choose from the list of functions you've added to your instance\.

1. \(Optional\) Under **Function input parameters**, choose **Add a parameter**\. You can specify key\-value pairs that are sent to the Lambda function when it is invoked\. You can also specify a **Timeout** value for the function\.

1. In **Timeout \(max 8 seconds\)**, specify how long to wait for Lambda to time out\. After this time, the contact routes down the Error branch\.

For every Lambda function invocation from a contact flow, you pass a default set of information related to ongoing contact, as well as any additional attributes defined in the **Function input parameters** section for the **Invoke AWS Lambda function** block added\.

The following is an example JSON request to a Lambda function:

```
{
    "Details": {
        "ContactData": {
            "Attributes": {},
            "Channel": "VOICE",
            "ContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXXX",
            "CustomerEndpoint": {
                "Address": "+1234567890",
                "Type": "TELEPHONE_NUMBER"
            },
            "InitialContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXXX",
            "InitiationMethod": "INBOUND | OUTBOUND | TRANSFER | CALLBACK",
            "InstanceARN": "arn:aws:connect:aws-region:1234567890:instance/c8c0e68d-2200-4265-82c0-XXXXXXXXXX",
            "PreviousContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXXX",
            "Queue": {
               "ARN": "arn:aws:connect:eu-west-2:111111111111:instance/cccccccc-bbbb-dddd-eeee-ffffffffffff/queue/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
               "Name": "PasswordReset"
             },
            "SystemEndpoint": {
                "Address": "+1234567890",
                "Type": "TELEPHONE_NUMBER"
            }
        },
        "Parameters": {
            "sentAttributeKey": "sentAttributeValue"
        }
    },
    "Name": "ContactFlowEvent"
}
```

The request is divided into three parts:
+ Contact data—This is always passed by Amazon Connect for every contact\. Some parameters are optional\.
+ User attributes—These are attributes that have been previously associated with a contact, such as when using a **Set contact attributes** block in a contact flow\. This map may be empty if there aren't any saved attributes\.
+ Parameters—These are parameters specific to this call that were defined when you created the Lambda function\.

### Invocation retry policy<a name="w463aac29c38c13c17"></a>

If your Lambda invocation in a contact flow gets throttled, the request will be retried\. It will also be retried if a general service failure \(500 error\) happens\. 

When a synchronous invocation returns an error, Amazon Connect retries up to 3 times, for a maximum of 8 seconds\. At that point, the flow will progress down the Error branch\. 

To learn more about how Lambda retries, see [Error Handling and Automatic Retries in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/retries-on-errors.html)\. 

### Invoke multiple Lambda functions<a name="invoke-multiple-functions"></a>

Amazon Connect limits the duration of a sequence of Lambda functions to 20 seconds\. It will error out when the total execution time exceeds this threshold\. Since customers hear silence while a Lambda function executes, we recommend adding a **Play prompt** block between functions to keep them engaged and aware of the long interaction\. 

By breaking up a chain of Lambda functions with the **Play prompt** block, you will be able invoke multiple functions that last longer than the 20 second threshold\.

## Configure your Lambda function to parse the event<a name="function-parsing"></a>

To successfully pass attributes between your Lambda function and Amazon Connect, configure your function to correctly parse the JSON request sent from the **Invoke AWS Lambda function** block, and define any business logic that should be applied\. How the JSON is parsed depends on the runtime you use for your function\. For example, the following example shows how to access `sentAttributeKey` using Node\.JS:

```
var receivedAttribute = event['Details']['Parameters']['sentAttributeKey'];
```

## Verify the function response<a name="verify-function"></a>

The Lambda function response should be a simple string map\. This map can be up to 32k\. If you fail to reach Lambda, the function throws an exception, the response is not understood, or the Lambda function takes more time than the limit, the contact flow jumps to the `Error` label\.

Test the output returned from your Lambda function to confirm that it will be correctly consumed when returned to Amazon Connect\. The following example shows a sample response in Node\.JS:

```
exports.handler = function(event, context, callback) {

var resultMap = {
    Name:'CustomerName',
    Address:'1234 Main Road',
    CallerType:'Patient'
}

callback(null, resultMap);
}
```

This example shows an example response using Python:

```
def lambda_handler(event, context):
    resultMap = {"Name":"CustomerName","Address":"1234 Main Road","CallerType":"Patient"}
    return resultMap
```

The output returned from the function must be a flat object of key/value pairs, with values that include only alphanumeric, dash, and underscore characters\. Nested and complex objects are not supported\. The size of the returned data must be less than 32 Kb of UTF\-8 data\.

The following example shows the JSON output from these Lambda functions:

```
{
    "Name": "CustomerName",
    "Address": "1234 Main Road",
    "CallerType": "Patient"
}
```

## Consume the Lambda function response<a name="process-function-response"></a>

There are two ways to use the function response in your contact flow\. You can either directly reference the variables returned from Lambda, or store the values returned from the function as contact attributes and then reference the stored attributes\. When you use an external reference to a response from a Lambda function, the reference will always receive the response from the most recently invoked function\. To use the response from a function before a subsequent function is invoked, the response must be saved as a contact attribute, or passed as a parameter to the next function\.

### Access variables directly<a name="access-variables"></a>

 If you access the variables directly, you can use them in contact flow blocks, but they are not included in contact trace records \(CTR\)\. To access these variables directly in a contact flow block, add the block after the **Invoke AWS Lambda function** block, and then reference the attributes as shown in the following example: 

```
Name - $.External.Name
Address - $.External.Address
CallerType - $.External.CallerType
```

Make sure that the name specified for the source attribute matches the key name returned from Lambda\.

### Store variables as contact attributes<a name="store-variables"></a>

If you store the variables as contact attributes, you can use them throughout your contact flow, and they are included in CTRs\.

To store the values returned as contact attributes and then reference them, use a **Set contact attributes** block in your contact flow after the **Invoke AWS Lambda function** block\. Choose **External** for the **Type**\. Following the example we're using, set **Destination key** to `returnedContactName`, and set the **Source attribute** to `Name`

Add Address as a **Source attribute** and use `returnedContactAddress` as the **Destination key**\. Then add `CallerType` as a **Source attribute** and use `returnedContactType` for the **Destination key**\.

Make sure that the name specified for the source attribute matches the key name returned from Lambda\.