# Flow block: Hold customer or agent<a name="hold-customer-agent"></a>

## Description<a name="hold-customer-agent-description"></a>
+ Places a customer or agent on or off hold\. This is useful when, for example, you want to put the agent on hold while the customer enters their credit card information\. 
+ If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\.

## Supported channels<a name="hold-customer-agent-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Flow types<a name="hold-customer-agent-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Outbound Whisper flow
+ Transfer to Agent flow 
+ Transfer to Queue flow

## Properties<a name="hold-customer-agent-properties"></a>

The following image shows the **Properties** page of the **Hold customer or agent** block\. It shows that the dropdown list has three options: **Agent on hold**, **Customer on hold**, and **Conference all**\.

![\[The properties page of the Hold customer or agent block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hold-customer-or-agent-properties.png)

These options are defined as follows:
+ **Agent on hold** = customer is on the call
+ **Conference all** = agent and customer are on the call
+ **Customer on hold** = agent is on the call

## Configured block<a name="hold-customer-agent-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It configured for **Agent on hold**, and it has two branches: **Success** and **Error**\.

![\[A configured Hold customer or agent block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hold-customer-or-agent-configured.png)

## Samples flows<a name="hold-customer-agent-samples"></a>

[Sample secure input with agent](sample-secure-input-with-agent.md) 