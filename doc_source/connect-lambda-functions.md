# Invoke AWS Lambda functions<a name="connect-lambda-functions"></a>

Amazon Connect can interact with your own systems and take different paths in flows dynamically\. To achieve this, invoke AWS Lambda functions in a flow, fetch the results, and call your own services or interact with other AWS data stores or services\. For more information, see the [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/)\.

To invoke a Lambda function from a flow, complete the following tasks\.

**Topics**
+ [Create a Lambda function](#create-lambda-function)
+ [Add a Lambda function to your Amazon Connect instance](#add-lambda-function)
+ [Invoke a Lambda function from a flow](#function-contact-flow)
+ [Configure your Lambda function to parse the event](#function-parsing)
+ [Verify the function response](#verify-function)
+ [Consume the Lambda function response](#process-function-response)
+ [Tutorial: Create a Lambda function and invoke in a flow](#tutorial-invokelambda)

## Create a Lambda function<a name="create-lambda-function"></a>

Create a Lambda function, using any runtime, and configure it\. For more information, see [Get started with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/get-started.html) in the *AWS Lambda Developer Guide*\.

If you create the Lambda function in the same Region as your contact center, you can use the Amazon Connect console to add the Lambda function to your instance as described in the next task, [Add a Lambda function to your Amazon Connect instance](#add-lambda-function)\. This automatically adds resource permissions that allow Amazon Connect to invoke the Lambda function\. Otherwise, if the Lambda function is in a different Region, you can add it to your flow using the flow designer and add the resource permissions using the [add\-permission](https://docs.aws.amazon.com/cli/latest/reference/lambda/add-permission.html) command, with a principal of `connect.amazonaws.com` and the ARN of your Amazon Connect instance\. For more information, see [Using Resource\-Based Policies for AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html) in the *AWS Lambda Developer Guide*\.

## Add a Lambda function to your Amazon Connect instance<a name="add-lambda-function"></a>

Before you can use an Lambda function in a flow, you need to add it to your Amazon Connect instance\.

**Add a Lambda function to your instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose your instance name in the **Instance Alias** column\. This instance name appears in the URL you use to access Amazon Connect\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Flows**\.

1. In the **AWS Lambda** section, use the **Function** drop\-down box to select the function to add to your instance\.
**Tip**  
The drop\-down lists only those functions in the same Region as your instance\. If no functions are listed, choose **Create a new Lambda function**, which opens the AWS Lambda console\.  
To use a Lambda in a different Region or account, in the [Invoke AWS Lambda function](invoke-lambda-function-block.md), under **Select a function**, you can enter the ARN of a Lambda\. Then set up the corresponding resource\-based policy on that Lambda to allow the flow to call it\.   
To call `lambda:AddPermission`, you need to:  
Set the principal to **connect\.amazonaws\.com**
Set the source account to be the account your instance is in\.
Set the source ARN to the ARN of your instance\.
For more information, see [Granting function access to other accounts](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html#permissions-resource-xaccountinvoke)\.

1. Choose **Add Lambda Function**\. Confirm that the ARN of the function is added under **Lambda Functions**\.

Now you can refer to that Lambda function in your flows\.

## Invoke a Lambda function from a flow<a name="function-contact-flow"></a>

1. Open or create a flow\.

1. Add an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block \(in the **Integrate** group\) to the grid\. Connect the branches to and from the block\.

1. Choose the title of the [Invoke AWS Lambda function](invoke-lambda-function-block.md) block to open its properties page\.

1. Under **Select a function**, choose from the list of functions you've added to your instance\.

1. \(Optional\) Under **Function input parameters**, choose **Add a parameter**\. You can specify key\-value pairs that are sent to the Lambda function when it is invoked\. You can also specify a **Timeout** value for the function\.

1. In **Timeout \(max 8 seconds\)**, specify how long to wait for Lambda to time out\. After this time, the contact routes down the Error branch\.

For every Lambda function invocation from a flow, you pass a default set of information related to ongoing contact, as well as any additional attributes defined in the **Function input parameters** section for the **Invoke AWS Lambda function** block added\.

The following is an example JSON request to a Lambda function:

```
{
    "Details": {
        "ContactData": {
            "Attributes": {
               "exampleAttributeKey1": "exampleAttributeValue1"
              },
            "Channel": "VOICE",
            "ContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXXX",
            "CustomerEndpoint": {
                "Address": "+1234567890",
                "Type": "TELEPHONE_NUMBER"
            },
            "CustomerId": "someCustomerId",
            "Description": "someDescription",
            "InitialContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXXX",
            "InitiationMethod": "INBOUND | OUTBOUND | TRANSFER | CALLBACK",
            "InstanceARN": "arn:aws:connect:aws-region:1234567890:instance/c8c0e68d-2200-4265-82c0-XXXXXXXXXX",
            "LanguageCode": "en-US",
            "MediaStreams": {
                "Customer": {
                    "Audio": {
                        "StreamARN": "arn:aws:kinesisvideo::eu-west-2:111111111111:stream/instance-alias-contact-ddddddd-bbbb-dddd-eeee-ffffffffffff/9999999999999",
                        "StartTimestamp": "1571360125131", // Epoch time value
                        "StopTimestamp": "1571360126131",
                        "StartFragmentNumber": "100" // Numberic value for fragment number 
                    }
                }
            },
            "Name": "ContactFlowEvent",
            "PreviousContactId": "4a573372-1f28-4e26-b97b-XXXXXXXXXXX",
            "Queue": {
                   "ARN": "arn:aws:connect:eu-west-2:111111111111:instance/cccccccc-bbbb-dddd-eeee-ffffffffffff/queue/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                 "Name": "PasswordReset"
                "OutboundCallerId": {
                    "Address": "+12345678903",
                    "Type": "TELEPHONE_NUMBER"
                }
            },
            "References": {
                "key1": {
                    "Type": "url",
                    "Value": "urlvalue"
                }
            },
            "SystemEndpoint": {
                "Address": "+1234567890",
                "Type": "TELEPHONE_NUMBER"
            }
        },
        "Parameters": {"exampleParameterKey1": "exampleParameterValue1",
               "exampleParameterKey2": "exampleParameterValue2"
        }
    },
    "Name": "ContactFlowEvent"
}
```

The request is divided into two parts:
+ Contact data—This is always passed by Amazon Connect for every contact\. Some parameters are optional\.

  This section may include attributes that have been previously associated with a contact, such as when using a **Set contact attributes** block in a flow\. This map may be empty if there aren't any saved attributes\.

  The following image shows where these attributes would appear in the properties page of a **Set contact attributes**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-setAttribute.png)
+ Parameters—These are parameters specific to this call that were defined when you created the Lambda function\. The following image shows where these parameters would appear in the properties page of the **Invoke AWS Lambda function** block\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-setParameter.png)

### Invocation retry policy<a name="retry"></a>

If your Lambda invocation in a flow gets throttled, the request will be retried\. It will also be retried if a general service failure \(500 error\) happens\. 

When a synchronous invocation returns an error, Amazon Connect retries up to 3 times, for a maximum of 8 seconds\. At that point, the flow will progress down the Error branch\. 

To learn more about how Lambda retries, see [Error Handling and Automatic Retries in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/retries-on-errors.html)\. 

### Invoke multiple Lambda functions<a name="invoke-multiple-functions"></a>

Customers hear silence while a Lambda function executes\. We recommend adding a **Play prompt** block between functions to keep customers engaged and aware of the long interaction\. 

## Configure your Lambda function to parse the event<a name="function-parsing"></a>

To successfully pass attributes and parameters between your Lambda function and Amazon Connect, configure your function to correctly parse the JSON request sent from the **Invoke AWS Lambda function** block or **Set contact attributes**, and define any business logic that should be applied\. How the JSON is parsed depends on the runtime you use for your function\. 

For example, the following code shows how to access `exampleParameterKey1` from **Invoke AWS Lambda function** block and `exampleAttributeKey1` from **Set contact attributes** block using Node\.JS:

```
exports.handler = function(event, context, callback) {
// Example: access value from parameter (Invoke AWS Lambda function)
let parameter1 = event['Details']['Parameters']['exampleParameterKey1'];
  		  
// Example: access value from attribute (Set contact attributes block)
let attribute1 = event['Details']['ContactData']['Attributes']['exampleAttributeKey1'];
  		  
// Example: access customer's phone number from default data
let phone = event['Details']['ContactData']['CustomerEndpoint']['Address'];
  		  
// Apply your business logic with the values
// ...
}
```

## Verify the function response<a name="verify-function"></a>

The Lambda function response should be a simple string map\. This map can be up to 32k\. If you fail to reach Lambda, the function throws an exception, the response is not understood, or the Lambda function takes more time than the limit, the flow jumps to the `Error` label\.

Test the output returned from your Lambda function to confirm that it will be correctly consumed when returned to Amazon Connect\. The following example shows a sample response in Node\.JS:

```
exports.handler = function(event, context, callback) {
// Extract data from the event object	     
let phone = event['Details']['ContactData']['CustomerEndpoint']['Address'];    
	   
// Get information from your APIs

let customerAccountId = getAccountIdByPhone(phone);
let customerBalance = getBalanceByAccountId(customerAccountId);
  		  
    let resultMap = {
        AccountId: customerAccountId,
        Balance: '$' + customerBalance,
}

callback(null, resultMap);
}
```

This example shows an example response using Python:

```
def lambda_handler(event, context):
// Extract data from the event object
  phone = event['Details']['ContactData']['CustomerEndpoint']['Address']
  		  
// Get information from your APIs
  customerAccountId = getAccountIdByPhone(phone)
  customerBalance = getBalanceByAccountId(customerAccountId)
  		  
  	resultMap = {
  		"AccountId": customerAccountId,
  		"Balance": '$%s' % customerBalance
  		}
        
 return resultMap
```

The output returned from the function must be a flat object of key/value pairs, with values that include only alphanumeric, dash, and underscore characters\. Nested and complex objects are not supported\. The size of the returned data must be less than 32 KB of UTF\-8 data\.

The following example shows the JSON output from these Lambda functions:

```
{
"AccountId": "a12345689",
"Balance": "$1000"
}
```

You may return any result as long as they are simple key\-value pairs\.

## Consume the Lambda function response<a name="process-function-response"></a>

There are two ways to use the function response in your flow\. You can either directly reference the variables returned from Lambda, or store the values returned from the function as contact attributes and then reference the stored attributes\. When you use an external reference to a response from a Lambda function, the reference will always receive the response from the most recently invoked function\. To use the response from a function before a subsequent function is invoked, the response must be saved as a contact attribute, or passed as a parameter to the next function\.

### 1\. Access variables directly<a name="access-variables"></a>

 If you access the variables directly, you can use them in flow blocks, but they are not included in contact records\. To access these variables directly in a flow block, add the block after the **Invoke AWS Lambda function** block, and then reference the attributes as shown in the following example: 

```
Name - $.External.Name
Address - $.External.Address
CallerType - $.External.CallerType
```

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-useExternal.png)

Make sure that the name specified for the source attribute matches the key name returned from Lambda\.

### 2\. Store variables as contact attributes<a name="store-variables"></a>

If you store the variables as contact attributes, you can use them throughout your flow, and they are included in contact records\.

To store the values returned as contact attributes and then reference them, use a **Set contact attributes** block in your flow after the **Invoke AWS Lambda function** block\. Choose **Use attribute**, **External** for the **Type**\. Following the example we're using, set **Destination Attribute** to `MyAccountId`, and set the **attribute** to `AccountId`, and do the same for `MyBalance` and **Balance**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-useInSetAttributes.png)

Add Address as a **Source attribute** and use `returnedContactAddress` as the **Destination key**\. Then add `CallerType` as a **Source attribute** and use `returnedContactType` for the **Destination key**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-useAttributeInPlayPrompt.png)

Make sure that the name specified for the source external attribute matches the key name returned from Lambda\.

## Tutorial: Create a Lambda function and invoke in a flow<a name="tutorial-invokelambda"></a>

### Step 1: Create the Lambda example<a name="tutorial-invokelambda-step1"></a>

1. Sign in to the AWS Management Console and open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. In AWS Lambda, choose **Create function**\.

1. Choose **Author from scratch**, if it's not selected already\. Under **Basic information**, for **Function name**, enter **MyFirstConnectLambda**\. For all other options, accept the defaults\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambdafunctions-tutorial-create-function-name.png)

1. Choose **Create function**\.

1. In the **Code source** box, in the **index\.js** tab, delete the template code from the code editor\.

1. Copy and paste the following code into the code editor as shown in the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambdafunctions-tutorial-code-source.png)

   ```
   exports.handler = async (event, context, callback) => {
   // Extract information
           const customerNumber = event.Details.ContactData.CustomerEndpoint.Address;
           const companyName = event.Details.Parameters.companyName;
   // Fetch data
           const balance = await fetchBalance(customerNumber, companyName);
           const support = await fetchSupportUrl(companyName);
   // Prepare result
           const resultMap = {
           customerBalance: balance,
           websiteUrl: support
           }
           callback(null, resultMap);
           }
           
           async function fetchBalance(customerPhoneNumber, companyName) {
   // Get data from your API Gateway or Database like DynamoDB
           return Math.floor(Math.random() * 1000);
           }
           
           async function fetchSupportUrl(companyName) {
   // Get data from your API Gateway or Database like DynamoDB
           return 'www.GGG.com/support';
           }
   ```

   This code is going to generate a random result for the customerBalance\.

1. Choose **Deploy**\.

1. After you choose **Deploy**, choose **Test** to launch the test editor\.

1. In the **Configure test event** dialog box, select **Create new event**\. For **Event name**, enter **ConnectMock** as the test name\.

1. In the **Event JSON** box, delete the sample code and enter the following code instead\. 

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
       "companyName": "GGG"
       }
   },
   "Name": "ContactFlowEvent"
   }
   ```

1. Choose **Save**\.

1. Choose **Test**\. You should see the following something similar to the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambdafunctions-tutorial-code-source-response.png)

   Your balance will be different\. The code generates a random number\.

### Step 2: Add your Lambda to Amazon Connect<a name="tutorial-invokelambda-step2"></a>

1. Go to the Amazon Connect console, at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\. 

1. Choose your Amazon Connect instance alias\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. On the navigation menu, choose **Flows**\.

1. In the AWS Lambda section, use the **Lambda Functions** dropdown box to select **MyFirstConnectLambda**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-add-myfirstconnectlambda.png)

1. Choose **Add Lambda Function**\.

### Step 3: Create the contact flow<a name="tutorial-invokelambda-step3"></a>

The following image is an example of the flow you are going to build using the steps in this procedure\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow.png)

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.

1. On the navigation menu, go to **Routing**, **Flows**, **Create a contact flow**\.

1. Drag a [Set contact attributes](set-contact-attributes.md) block onto the grid, and configure its properties page shown in the following image:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow-set-contact-attribute-1.png)

   1. **Namespace** = **User defined**\.

   1. **Attribute** = **companyName**\.

   1. Choose **Set manually**\. **Value** = **GGG**\.

   1. Choose **Save**\.

1. Drag a [Play prompt](play.md) block onto the grid, and configure its properties page as shown in the following image:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow-play-prompt-1.png)

   1. Choose **Text\-to\-speech or chat text**, **Set manually**, and set **Interpret as** to **SSML**\. Enter the following text in the box for the text to be spoken:

      `Hello, thank you for calling $.Attributes.companyName inc.`

   1. Choose **Save**\.

1. Drag another [Play prompt](play.md) block onto the grid, and configure its properties page as shown in the following image:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow-play-prompt-2.png)

   1. Choose **Text\-to\-speech or chat text**, **Set manually**, and set **Interpret as** to **Text**\. Enter the following text in the box for the text to be spoken:

      `Please try again later.`

   1. Choose **Save**\.

1. Drag a [Invoke AWS Lambda function](invoke-lambda-function-block.md) block onto the grid, and configure its properties page as shown in the following image:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow-invoke-lambda.png)

   1. Choose **Select manually**, and then choose **MyFirstConnectLambda** from the dropdown\.

   1. In the **Destination Key** box, enter **companyName**\. \(This is sent to Lambda\.\)

   1. Choose **Set dynamically** box

   1. For **Namespace**, select **User Defined**\.

   1. For **Attribute**, enter **companyName**\.

   1. Choose **Save**\.

1. Drag a [Set contact attributes](set-contact-attributes.md) block onto the grid, choose **Add another attribute**, and configure its properties page as shown in the following image:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow-set-contact-attribute-2.png)

   1. **Namespace** = **User Defined**\. **Attribute** = **MyBalance**\.

   1. Choose **Set dynamically**\. 

   1. **Namespace** = **External**\.

   1. **Attribute** = **customerBalance**\. This is the result from Lambda\.

   1. Choose **Add another attribute**\.

   1. **Namespace** = **User\-defined**\.

   1. **Attribute** = **MyURL**\.

   1. Select **Set dynamically**\. **Namespace** =**External**\. 

   1. **Attribute** = **websiteUrl**\. This is the result from Lambda\.

   1. Choose **Save**\.

1. Drag a [Play prompt](play.md) block onto the grid, and configure its properties page as shown in the following image:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lambda-exampleFlow-play-prompt-3.png)

   1. Choose **Text\-to\-speech or chat text**, and set **Interpret as** to **SSML**\. Enter the following text in the box:

      `Your remaining balance is <say-as interpret-as="characters">$.Attributes.MyBalance</say-as>.`

      `Thank you for calling $.Attributes.companyName.`

      `Visit $.Attributes.MyURL for more information.`

   1. Choose **Save**\.

1. Drag a [Disconnect / hang up](disconnect-hang-up.md) block onto the grid\. 

1. Connect the all blocks so your flow looks like the image shown at the top of this procedure\.

1. Enter **MyFirstConnectFlow** as the name, and then choose **Publish**\.

1. On the navigation menu, go to **Channels**, **Phone numbers**\. 

1. Select your phone number\.

1. Select **MyFirstConnectFlow** and choose **Save**\.

Now try it out\. Call the number\. You should hear a greeting message, your balance, and the website to visit\.