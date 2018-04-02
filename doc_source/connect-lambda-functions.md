# Using AWS Lambda Functions with Amazon Connect<a name="connect-lambda-functions"></a>

Amazon Connect can interact with your own systems and take different paths in contact flows dynamically\. To achieve this, invoke Lambda functions, fetch results in an contact flow, and call your own services or interact with other AWS data stores or services\.

To learn more about AWS Lambda, see the [AWS Lambda Developer Guide](http://docs.aws.amazon.com/lambda/latest/dg/)\.

## Invoking a Lambda Function from a Contact Flow<a name="allow-call-function"></a>

The steps required to invoke a Lambda function from Amazon Connect include the following:

1. Create a Lambda function and define its trigger policy to allow Amazon Connect to invoke the function\.

1. Use the ARN of the Lambda function in an **Invoke AWS Lambda function** block in your contact flow\.

1. Configure the Lambda function code to parse the JSON event sent from the contact flow, and define the business logic to execute\.

1. Test the configuration to confirm that the Lambda function returns the correct JSON response\.

1. Consume the attribute values returned from Lambda to use in your contact flow\.

### Create a Lambda Function and Configure a Trigger Policy<a name="lambda-policy"></a>

Amazon Connect can successfully invoke a Lambda function in an AWS account when a resource policy has been set on the Lambda function\. For more information, see [Using Resource\-Based Policies for AWS Lambda](http://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html) in the *AWS Lambda Developer Guide*\.

To begin, create a Lambda function, and then note down the function name\. For more information about creating a Lambda function, see [Create a Simple Lambda Function](http://docs.aws.amazon.com/lambda/latest/dg/get-started-create-function.html)\.

Use the following [add\-permission](http://docs.aws.amazon.com/cli/latest/reference/lambda/add-permission.html) command to create a resource policy using this information:

```
aws lambda add-permission --function-name function:my-lambda-function --statement-id 1 \
--principal connect.amazonaws.com  --action lambda:InvokeFunction --source-account 123456789012 \
--source-arn arn:aws:connect:us-east-1:123456789012:instance/def1a4fc-ac9d-11e6-b582-06a0be38cccf \
```

This command uses the following input:
+ The name of the Lambda function \(for example, **my\-lambda\-function**\)
+ The ARN of a Amazon Connect instance \(for example, **arn:aws:connect:us\-east\-1:123456789012:instance/def1a4fc\-ac9d\-11e6\-b582\-example**\)

  To find the ARN for your instance, open the [Amazon Connect console](https://console.aws.amazon.com/connect), and then choose the **Instance Alias** to open the **Overview** page\.
+ The AWS account ID for the Lambda function \(for example, **123456789012**\)

### Invoke the Lambda Function in Your Contact Flow<a name="funtion-contact-flow"></a>

To invoke a Lambda function from your contact flow, add an **Invoke AWS Lambda function** block to the flow, and then add the ARN for the function you created as the value for the **Function ARN** in the contact flow properties\. You can view the ARN for the function in the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

You can also run the following command in the AWS Command Line Interface to view the function ARN:

```
aws lambda get-function --function-name my-lambda-function
```

In the **Invoke AWS Lambda function** block, you can add **Function input parameters**, which are key\-value pairs that are sent to the Lambda function when invoked\. You can also specify a **Timeout** value for the function\.

On every Lambda function invocation from a contact flow, you pass a default set of information related to ongoing contact, as well as any additional attributes defined in the **Function input parameters** for the **Invoke AWS Lambda function** block added to your contact flow\.

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
            "PreviousContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXX",
            "Queue": "QueueName",
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

The Lambda function response should be a simple Map *String String*\. This map can be up to 32k\. If you fail to reach Lambda, the function throws an exception, the response is not understood, or the Lambda function takes more time than the limit, the contact flow jumps to the `Error` label\. The following code is an example Python Lambda function:

### Configure Your Lambda Function<a name="function-parsing"></a>

To successfully pass attributes between your Lambda function and Amazon Connect, configure your function to correctly parse the JSON request sent from the **Invoke AWS Lambda function** block, and define any business logic that should be applied\. How the JSON is parsed depends on the runtime you use for your function\. For example, the following example shows how to access the sentAttributeKey using sing Node\.JS:

```
var receivedAttribute = event['Details']['Parameters']['sentAttributeKey'];
```

### Verify the Function Response<a name="verify-function"></a>

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

And this example shows an example response using Python:

```
def lambda_handler(event, context):
resultMap = {"Name":"CustomerName","Address":"1234 Main Road","CallerType":"Patient"};
return resultMap;
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

### Using the Lambda Function Response<a name="process-function-response"></a>

There are two ways to use the function response in your contact flow\. You can either directly reference the variables returned from Lambda, or store the values returned from the function as contact attributes and then reference the stored attributes\. When you use an external reference to a response from a Lambda function, the reference will always receive the response form the most recently invoked function\. To use the response from a function before a subsequent function is invoked, the response must be saved as a contact attribute, or passed as a parameter to the next function\.

**Access Lambda attributes directly**  
If you access the variables directly, you can use them in contact flow blocks, but they are not included in CTRs\. To access these variables directly in a contact flow block, add the block after the **Invoke AWS Lambda function** block, and then reference the attributes as shown in the following example: 

```
Name - $.External.Name
Address - $.External.Address
CallerType - $.External.CallerType
```

Make sure that the name specified for the source attribute matches the key name returned from Lambda\.

**Store Lambda variables as contact attributes**  
If you store the variables as contact attributes, you can use them throughout your contact flow, and they are included in CTRs\.

To store the values returned as contact attributes and then reference them, use a **Set contact attributes** block in your contact flow after the **Invoke AWS Lambda function** block\. Choose **External** for the **Type**\. Following the example we're using, set **Destination key** to `returnedContactName`, and set the **Source attribute** to `Name`

Add Address as a **Source attribute** and use `returnedContactAddress` as the **Destination key**\. Then add callerType as a **Source attribute** and use `returnedContactType` for the **Destination key**\.

Make sure that the name specified for the source attribute matches the key name returned from Lambda\.