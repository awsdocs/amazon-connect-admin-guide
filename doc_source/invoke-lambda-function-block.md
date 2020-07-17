# Contact block: Invoke AWS Lambda function<a name="invoke-lambda-function-block"></a>

## Contact flow types<a name="invoke-lambda-function-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Customer Hold flow
+ Customer Whisper flow
+ Agent Hold flow
+ Agent Whisper flow
+ Transfer to Agent flow 
+ Transfer to Queue flow

## Description<a name="invoke-lambda-function-block-description"></a>
+ Calls AWS Lambda, and optionally returns key\-value pairs\.
+ The returned key\-value pairs can be used to set contact attributes\.

## Properties<a name="invoke-lambda-function-block-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/invoke-lambda-properties.png)

Note the following properties: 
+ **Timeout**: Enter how long to wait for Lambda to time out\. This creates a branch for you to specify what to do if it times out\. 

  If your Lambda invocation gets throttled, the request is retried\. It is also retried if a general service failure \(500 error\) happens\. 

  When a synchronous invocation returns an error, Amazon Connect retries up to three times, for a maximum of 8 seconds\. At that point, the contact is routed down the **Error** branch\.

## Configuration tips<a name="invoke-lambda-function-block-tips"></a>
+ To use an AWS Lambda function in a contact flow, first add the function to your instance\. For more information, see [Add a Lambda function to your Amazon Connect instance](connect-lambda-functions.md#add-lambda-function), 
+ After you add the function to your instance, you can select the function from the **Select a function** drop\-down list in the block to use it in the contact flow\.

## Configured block<a name="invoke-lambda-function-block-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/invoke-lambda-configured.png)

## Sample flows<a name="invoke-lambda-function-block-samples"></a>

[Sample Lambda integration](sample-lambda-integration.md)

## Scenarios<a name="invoke-lambda-function-block-scenarios"></a>

See these topics for scenarios that use this block:
+ [Invoke AWS Lambda functions](connect-lambda-functions.md)