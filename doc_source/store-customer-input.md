# Contact block: Store customer input<a name="store-customer-input"></a>

## Contact flow types<a name="store-customer-input-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="store-customer-input-description"></a>

This block is similar to **Get customer input**, but this one stores the input as a contact attribute and allows you to encrypt it\. This way, you can encrypt sensitive input such as credit card numbers\. This block:
+ Plays an interruptible prompt to get a response from the customer\. For example, "Please enter your credit card number" or "Please enter the phone number we should use to call you back\." 
+ Plays an interruptible audio prompt or play text\-to\-speech for a customer to respond to\. 
+ Stores numerical input as a contact attribute\.
+ Allows you to specify a custom terminating keypress\.
+ If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\.

## Properties<a name="store-customer-input-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input-properties1.png)

Note the following properties:
+ **Maximum Digits**: Define the maximum number of digits that a customer can enter\. 
+ **Timeout before first entry**: Specify how long to wait for a customer to start entering their reply by voice\. For example, you might enter 20 seconds, to give the customer time to get their credit card\.

  After the contact starts entering digits, Amazon Connect waits 5 seconds for each digit, by default\. You cannot change this default setting\. 
+ **Encrypt entry**: Encrypt the customer's entry, such as their credit card information\. For step\-by\-step instructions to get the keys that you use to input this information, see [Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)\.
+ **Specify terminating keypress**: Define a custom terminating keypress that is used when your contacts complete their DTMF inputs\. The terminating keypress can be up to five digits long, with \#, \* and 0\-9 characters, instead of just \#\. 
+ **Disable cancel key**: By default, when a customer enters \* as input, it deletes all of the DTMF input that came before it\. However, if you choose **Disable cancel key**, Amazon Connect treats the **\*** as any other key\.

  If you send the DMTF input to an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block, the **Disable cancel key** property affects the input, as follows: 
  + When **Disable cancel key** is selected, all the characters entered—including any \*—are sent to the **Invoke Lambda function** block\. 
  + When **Disable cancel key** is not selected, only the \* is sent to the **Invoke Lambda function** block\. 

  For example, let's say you chose **Disable cancel key**, and a customer entered *1\#2\#3\*4\#\#\#*, where *\#\#* is the terminating keypress\. The **Invoke Lambda function** block then receives the entire *1\#2\#3\*4\#* as input\. You could program the Lambda function to ignore the character before the \* character\. So, the customer input would be interpreted as *1\#2\#4\#*\.
+ **Phone number**: This option is useful for queued callback scenarios\.
  + **Local format**: If all of your customers all calling from the same country that your instance is in, choose that country from the dropdown list\. Amazon Connect then auto\-populates the country code for customers so that they don't have to enter it\.
  + **International format**: If you have customers calling from different countries, choose **International format**\. Amazon Connect then requires customers to enter their country code\.

## Configuration tips<a name="store-customer-input-tips"></a>

To use a star \(\*\) as part of the terminating keypress, you must also choose **Disable cancel key**\.

## Configured block<a name="store-customer-input-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input-configured.png)

## Sample flows<a name="store-customer-input-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample secure input with agent](sample-secure-input-with-agent.md)
+ [Sample secure input with no agent](sample-secure-input-with-noagent.md) 
+ [Sample queue configurations](sample-queue-configurations.md) 
+ [Sample queued callback](sample-queued-callback.md) 

## Scenarios<a name="store-customer-input-scenarios"></a>

[Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)