# Contact Block: Get Customer Input<a name="get-customer-input"></a>

## In contact flow types<a name="get-customer-input-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Generic contact flow
+ Customer queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="get-customer-input-description"></a>
+ It plays a prompt to get a response from the customer\. For example, "Press 1 for Sales, press 2 for Support\." 
+ When customers enter DTMF input, the prompt is interruptible\. 
+ When an Amazon Lex bot plays a voice prompt, customers can interrupt it with their voice\. To set this up, use the `barge-in-enabled` session attribute\.
+ It then branches based on the customer's input\.
+ This block works for chat only when Amazon Lex is used\.

## Properties<a name="get-customer-input-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-customer-input.png)

You can configure this block to accept DTMF input, a chat response, or an Amazon Lex intent\.

**DTMF tab properties**
+ **Audio prompt**: Select from a list of default audio prompts, or upload your own audio prompt\. 
+ **Set timeout**: Specify how long to wait while the user decides how they want to respond to the prompt\.

**Amazon Lex tab properties**
+ **Lex bot properties**: After you create your Lex bot, enter the name and alias of the bot here\. Only published bots appear in the drop\-down list\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-customer-input-properties2.png)
+ **Session attributes**: Specify attributes that apply to the current contact's session only\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-customer-input-properties3.png)

**Configurable time\-outs for voice input**

To configure time\-out values for voice contacts, use the following session attributes in the **Get customer input** block that calls your Lex bot\. These attributes allow you to specify how long to wait for the customer to finish speaking before Amazon Lex collects speech input from callers, such as answering a yes/no question, or providing a date or credit card number\. 
+ **Max Speech Duration**

  `x-amz-lex:max-speech-duration-ms:[intentName]:[slotToElicit]`

  How long the customer speaks before the input is truncated and returned to Amazon Connect\. You can increase the time when a lot of input is expected or you want to give customers more time to provide information\. 

  Default = 13000 milliseconds \(13 seconds\)\. The maximum allowed value is 15000 milliseconds\. 
**Important**  
If you set **Max Speech Duration** to more than 15000 milliseconds, the contact is routed down the **Error** branch\. 
+ **Start Silence Threshold**

   `x-amz-lex:start-silence-threshold-ms:[intentName]:[slotToElicit]`

  How long to wait before assuming that the customer isn't going to speak\. You can increase the allotted time in situations where you’d like to allow the customer more time to find or recall information before speaking\. For example, you might want to give customers more time to get out their credit card so they can enter the number\. 

  Default = 4000 milliseconds \(4 seconds\)\.
+ **End Silence Threshold**

  `x-amz-lex:end-silence-threshold-ms:[intentName]:[slotToElicit]` 

  How long to wait after the customer stops speaking before assuming the utterance has concluded\. You can increase the allotted time in situations where periods of silence are expected while providing input\. 

  Default = 600 milliseconds \(0\.6 seconds\)

 **Barge\-in configuration and usage for Amazon Lex**

You can allow customers to interrupt the Amazon Lex bot mid\-sentence using their voice, without waiting for it to finishing speaking\. Customers familiar with choosing from a menu of options, for example, can now do so, without having to listen to the entire prompt\.

To set up this functionality, set the `barge-in-enabled` session attribute in the **Get customer input** block that calls your Lex bot\. This attribute only controls Amazon Lex barge\-in; it doesn't control DTMF barge\-in\. 
+ **Barge\-in**

  `x-amz-lex:barge-in-enabled:[intentName]:[slotToElicit]`

  Barge\-in is disabled globally by default\. You must set the session attribute to enable it at the global, bot, or slot levels\. For more information, see [How to Use Lex Session Attributes](how-to-use-session-attributes.md)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/barge-in-session-attribute.png)

**Intents**
+ Enter the intents you created in Amazon Lex\. They are case sensitive\!  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input3.png)

## Configuration tips<a name="get-customer-input-tips"></a>
+ When you use text, either for text\-to\-speech or chat, you can use a maximum of 3,000 billed characters \(6,000 total characters\)\.
+ Amazon Lex bots support both spoken utterances and keypad input when used in a contact flow\.
+ You can prompt contacts to end their input with a pound key \# and to cancel it using the star key \*\. 
+ To control time\-out  functionality, you can use Lex session attributes in this block, or in set them in your Lex Lambda function\. If you choose to set the attributes in a Lex Lambda function, the default values are used until the Lex bot is invoked\. For more information, see [Using Lambda Functions](https://docs.aws.amazon.com/lex/latest/dg/using-lambda.html) in the *Amazon Lex Developer Guide*\. 
+ When you specify one of the session attributes described in this article, you can use wildcards\. They let you set multiple slots for an intent or bots\.

  Following are some examples of how you can use wildcards:
  + To set all slots for a specific intent, such as PasswordReset, to 2000 milliseconds:

    Name = `x-amz-lex:max-speech-duration-ms:PasswordReset:*`

    Value = 2000
  + To set all slots for all bots to 4000 milliseconds: 

    Name = `x-amz-lex:max-speech-duration-ms:*:*`

    Value = 4000

  Wildcards apply across bots but not across blocks in a contact flow\. 

  For example, you have a Get\_Account\_Number bot\. In the contact flow, you have two **Get customer input** blocks\. The first block sets the session attribute with a wildcard\. The second one doesn't set the attribute\. In this scenario, the change in behavior for the bot applies only to the first **Get customer input** block, where the session attribute is set\. 
+ Because you can specify that session attributes apply to the intent and slot level, you can specify that the attribute is set only when you're collecting a certain type of input\. For example, you can specify a longer **Start Silence Threshold** when you're collecting an account number than when you're collecting a date\. 

## Configured block<a name="get-customer-input-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-customer-input-configured.png)

## Sample flows<a name="get-customer-input-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample Inbound Flow \(First Contact Experience\)](sample-inbound-flow.md)
+ [Sample Interruptible Queue Flow with Callback](sample-interruptible-queue.md) 
+ [Sample Queue Configurations](sample-queue-configurations.md) 
+ [Sample Recording Behavior](sample-recording-behavior.md) 

## Scenarios<a name="get-customer-input-scenarios"></a>

See these topics for scenarios that use this block:
+ [Add an Amazon Lex Bot](amazon-lex.md)
+ [How to Use the Same Bot for Voice and Chat](one-bot-voice-chat.md)
+ [Add Text\-to\-Speech to Prompts](text-to-speech.md)