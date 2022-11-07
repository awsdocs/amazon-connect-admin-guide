# Flow block: Store customer input<a name="store-customer-input"></a>

## Description<a name="store-customer-input-description"></a>

This block is similar to **Get customer input**, but this one stores the input as a contact attribute \(in the [Stored customer input](connect-attrib-list.md#attribs-system-table) system attribute\) and allows you to encrypt it\. This way, you can encrypt sensitive input such as credit card numbers\. This block:
+ Plays an interruptible prompt to get a response from the customer\. For example, "Please enter your credit card number" or "Please enter the phone number we should use to call you back\." 
+ Plays an interruptible audio prompt or play text\-to\-speech for a customer to respond to\. 
+ Stores numerical input as in the [Stored customer input](connect-attrib-list.md#attribs-system-table) system attribute\.
+ Allows you to specify a custom terminating keypress\.
+ If during a call the customer doesn't enter any input, the contact is routed down the **Success branch** branch with a value of Timeout\. Add a **Check contact attributes** block to check for timeouts\.

## Supported channels<a name="store-customer-input-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Flow types<a name="store-customer-input-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="store-customer-input-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input-properties1.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input-properties1b.png)

Note the following properties:
+ For information about choosing a prompt from the Amazon Connect library or an S3 bucket, see the [Play prompt](play.md) block\.
+ **Maximum Digits**: Define the maximum number of digits that a customer can enter\. 
+ **Timeout before first entry**: Specify how long to wait for a customer to start entering their reply by voice\. For example, you might enter 20 seconds, to give the customer time to get their credit card\.

  After the contact starts entering digits, Amazon Connect waits 5 seconds for each digit, by default\. You cannot change this default setting\. 
+ **Encrypt entry**: Encrypt the customer's entry, such as their credit card information\. For step\-by\-step instructions to get the keys that you use to input this information, see [Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)\.
+ **Specify terminating keypress**: Define a custom terminating keypress that is used when your contacts complete their DTMF inputs\. The terminating keypress can be up to five digits long, with \#, \* and 0\-9 characters, instead of just \#\. 
**Note**  
To use a star \(\*\) as part of the terminating keypress, you must also choose **Disable cancel key**\.
+ **Disable cancel key**: By default, when a customer enters \* as input, it deletes all of the DTMF input that came before it\. However, if you choose **Disable cancel key**, Amazon Connect treats the **\*** as any other key\.

  If you send the DMTF input to an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block, the **Disable cancel key** property affects the input, as follows: 
  + When **Disable cancel key** is selected, all the characters entered—including any \*—are sent to the **Invoke Lambda function** block\. 
  + When **Disable cancel key** is not selected, only the \* is sent to the **Invoke Lambda function** block\. 

  For example, let's say you chose **Disable cancel key**, and a customer entered *1\#2\#3\*4\#\#\#*, where *\#\#* is the terminating keypress\. The **Invoke Lambda function** block then receives the entire *1\#2\#3\*4\#* as input\. You could program the Lambda function to ignore the character before the \* character\. So, the customer input would be interpreted as *1\#2\#4\#*\.
+ **Phone number**: This option is useful for queued callback scenarios\.
  + **Local format**: If all of your customers all calling from the same country that your instance is in, choose that country from the dropdown list\. Amazon Connect then auto\-populates the country code for customers so that they don't have to enter it\.
  + **International format**: If you have customers calling from different countries, choose **International format**\. Amazon Connect then requires customers to enter their country code\.

## Problems with DTMF input?<a name="store-customer-input-use-multiple-input-blocks"></a>

Let's say you have the following scenario with two contacts flows, each one capturing DTMF input from customers: 

1. One flow uses the **Get customer input** block to request DTMF input from customers\.

1. After the DTMF input is entered, it uses the **Transfer to flow** block to move the contact to the next contact flow\.

1. In the next flow, there's a **Store customer input** block to get more DTMF input from the customer\.

There's setup time between the first and second flows\. This means if the customer enters DTMF input very quickly for the second flow, some of the DTMF digits might be dropped\.

For example, the customer needs to press 5, then wait for a prompt from the second flow, then type 123\. In this case, 123 is captured without problem\. However, if they don't wait for the prompt and enter 5123 very quickly, the **Store customer input** block may capture only 23 or 3\.

To guarantee the **Store customer input** block in second contact flow captures all of the digits, the customer needs to wait for the prompt to be played, and then enter their type DTMF input\.

## Configured block<a name="store-customer-input-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input-configured.png)

1. **Invalid number**: What to do if the customer enters an invalid number\.

## Sample flows<a name="store-customer-input-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample secure input with agent](sample-secure-input-with-agent.md)
+ [Sample secure input with no agent](sample-secure-input-with-noagent.md) 
+ [Sample queue configurations](sample-queue-configurations.md) 
+ [Sample queued callback](sample-queued-callback.md) 

## Scenarios<a name="store-customer-input-scenarios"></a>

[Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)