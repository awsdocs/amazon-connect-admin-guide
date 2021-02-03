# Contact block: Hold customer or agent<a name="hold-customer-agent"></a>

## Description<a name="get-queue-metrics-description"></a>
+ Places a customer or agent on or off hold\. This is useful when, for example, you want to put the agent on hold while the customer enters their credit card information\. 
+ If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\.

## Contact flow types<a name="get-queue-metrics-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Outbound Whisper flow
+ Transfer to Agent flow 
+ Transfer to Queue flow

## Properties<a name="get-queue-metrics-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hold-customer-or-agent-properties.png)

The following settings are available:
+ **Agent on hold** = customer is on the call
+ **Conference all** = agent and customer are on the call
+ **Customer on hold** = agent is on the call

## Configured block<a name="get-queue-metrics-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hold-customer-or-agent-configured.png)

## Samples flows<a name="get-queue-metrics-samples"></a>

[Sample secure input with agent](sample-secure-input-with-agent.md) 