# Contact block: Call phone number<a name="call-phone-number"></a>

## Description<a name="call-phone-number-description"></a>
+ Use to place an outbound call from an **Outbound Whisper** flow\.

## Contact flow types<a name="call-phone-number-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Outbound Whisper flow

## Properties<a name="call-phone-number-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-phone-number1.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-phone-number2.png)

Outbound whisper flows run in Amazon Connect immediately after an agent accepts the call during direct dial and callback scenarios\. When the contact flow runs: 
+ The caller ID number is set if one is specified in the [Call phone number](#call-phone-number) block\.
+ If no caller ID is specified in the [Call phone number](#call-phone-number) block, the caller ID number defined for the queue is used when the call is placed\.
+ When there is an error with a call that is initiated by the [Call phone number](#call-phone-number) block, the call is disconnected and the agent is placed in **AfterContactWork** \(ACW\)\.

Only published contact flows can be selected as the outbound whisper flow for a queue\.

## Configured block<a name="call-phone-number-configured-block"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/call-phone-number-configured.png)

There is no error branch for the block\. If a call is not successfully initiated, the contact flow ends and the agent is placed in an **AfterContactWork** \(ACW\)\. 

## Sample flows<a name="call-phone-number-sample-flows"></a>

See these sample flows for scenarios that use this block:
+ [Sample customer queue priority](sample-customer-queue-priority.md)
+  [Sample queue configurations](sample-queue-configurations.md)

## Scenarios<a name="call-phone-number-scenarios"></a>

See these topics for more information about caller ID works:
+ [Set up outbound caller ID](queues-callerid.md)