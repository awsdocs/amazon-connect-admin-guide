# Contact initiation methods and the types of contact flows run<a name="contact-initiation-methods"></a>

Every contact in your Amazon Connect contact center is initiated by one of the following methods: 
+ Inbound
+ Outbound
+ Transfer
+ Callback
+ API
+ Queue\_Transfer
+ Disconnect

You can create contact flows appropriate for a given initiation method when you know which [types of contact flows ](create-contact-flow.md#contact-flow-types) the initiation method uses\.

For each initiation method, this topic explains which types of contact flows are run\.

## Inbound<a name="inbound-initiation-method"></a>

The customer initiated a voice \(phone\) contact with your contact center\.
+ When the contact successfully connects with the phone number of your contact center, an [Inbound contact flow](create-contact-flow.md#contact-flow-types) is presented to caller\.
+ During the transition in the **Inbound contact flow**, if the customer is put in a queue, a [Customer queue flow](create-contact-flow.md#contact-flow-types) is played to customer\.
+ After the agent becomes available to handle the caller and accept the contact, a [Agent whisper flow](create-contact-flow.md#contact-flow-types) is played to the agent\.
+ After a [Agent whisper flow](create-contact-flow.md#contact-flow-types) completes, a [Customer whisper flow](create-contact-flow.md#contact-flow-types) is played to customer\.
+ After the both whisper flows are played successfully to the agent and the customer respectively, the caller gets connected to agent for interaction\.

To summarize, for a simple inbound call, the following contact flow types are played before caller is connected to agent: 

1. **Inbound contact flow**

1. **Customer queue flow**

1. **Agent whisper flow**

1. **Customer whisper flow**

## Outbound<a name="outbound-initiation-method"></a>

An agent initiated voice \(phone\) contact to an external number, by using their CCP to make the call\. 
+ As soon as the destination party picks the call, they are presented with an [Outbound whisper flow](create-contact-flow.md#contact-flow-types)\.
+ After an **Outbound whisper flow** successfully completes, the agent and the contact are connected for interaction\.

To summarize, an **Outbound contact flow** type is the only one involved in an outbound call initiated from Amazon Connect\.

## Transfer<a name="transfer-initiation-method"></a>

The contact was transferred by an agent to another agent or to a queue, using quick connects in the CCP\. This results in a new contact record being created\.

Before the agent transfers the contact to another agent or queue, all the flows involved in an INBOUND contact are run\.
+ Agent to Agent transfer using Agent Quick Connect
  + After the agent transfers the inbound contact to another agent:
    + A [Agent transfer flow](create-contact-flow.md#contact-flow-types) is played to the source agent\.
    + After the destination agent accepts the call, a [Agent whisper flow](create-contact-flow.md#contact-flow-types) is played to destination agent, and then a [Customer whisper flow](create-contact-flow.md#contact-flow-types) is played to source agent\.
    + After all three flows are successfully run, the interaction begins between the source and destination agents\.
    + During this whole process, the inbound caller is on hold and a [Customer hold flow](create-contact-flow.md#contact-flow-types) is played to the inbound caller during hold time\.

    After the source agent is connected with destination agent, the source agent can do one of the following actions:
    + Choose **Join**\. This joins all parties on the call: source agent, destination agent, and the customer are joined in a conference call\.
    + Choose **Hold all**\. This puts the destination agent and the customer on hold\. 
    + Put destination agent on hold, so only the source agent can talk to the customer\.
    + Choose **End call**\. The source agent leaves the call but the destination agent and the customer are directly connected and continue talking\.

  To summarize for an agent to agent transfer call, the following contact flow types are run:

  1. **Agent transfer flow**

  1. **Agent whisper flow** \(played to the destination agent\) 

  1. **Customer whisper flow** \(played to the source agent\) during whole this process

  1. **Customer hold flow** played to the original caller
+ Agent to Queue transfer using Queue Quick Connect
  + After the agent transfers the inbound call to another queue:
    + A [Queue transfer flow](create-contact-flow.md#contact-flow-types) is played to source agent\.
    + After the agent from the transferred queue accepts the call, an [Agent whisper flow](create-contact-flow.md#contact-flow-types) is played to destination agent, and then a [Customer whisper flow](create-contact-flow.md#contact-flow-types) is played to source agent\.
    + After these flows run, the source and destination agent interaction begins\.
    + During this whole process, the inbound caller is on hold\. A [Customer hold flow](create-contact-flow.md#contact-flow-types) is played to the inbound caller during the hold time\.

    After the source agent is connected with destination agent, the source agent can do one of the following:
    + Choose **Join**\. This joins all parties on the call: source agent, destination agent, and the customer are joined in a conference call\.
    + Choose **Hold all**\. This puts destination agent and the customer on hold\.
    + Put destination agent on hold, so only the source agent can talk to the customer\.
    + Choose **End call**\. The source agent leaves the call but the destination agent and the customer are directly connected and continue talking\.

  To summarize for agent to queue transfer call, the following contact flows are played: 

  1. **Queue transfer flow** 

  1. **Agent whisper flow** \(played to the destination agent\) 

  1. **Customer whisper flow** \(played to the source agent\) during whole this process

  1. **Customer hold flow** played to the original caller

## Callback<a name="callback-initiation-method"></a>

The customer is contacted as part of a callback flow\. 
+ As soon as agent accepts the callback contact, an [Agent whisper flow](create-contact-flow.md#contact-flow-types) is played to the agent\.
+ After the customer accepts the callback call, an [Outbound whisper flow](create-contact-flow.md#contact-flow-types) is played to customer\.
+ After these two flows are played, the agent and customer are connected and can interact\. 

To summarize, for callback contacts, the following contact flow types are played:
+ **Agent whisper flow**
+ **Outbound whisper flow**

## API<a name="api-initiation-method"></a>

 The contact was initiated with Amazon Connect by API\. This could be:

1. An outbound contact you created and queued to an agent using the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API\.

1. A live chat that was initiated by the customer with your contact center where you called the [StartChatConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API\.

1. A task that was initiated by calling the [StartTaskConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API\.

Following is an example of an API initiated contact method:
+ After the outbound contact is successfully initiated using the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API, an [Inbound contact flow](create-contact-flow.md#contact-flow-types) provided in the API request is played to the customer\.
+ Depending on the configuration of the [Inbound contact flow](create-contact-flow.md#contact-flow-types), additional contact flows are played\. For example, an [Inbound contact flow](create-contact-flow.md#contact-flow-types) transfers a customer to an agent for conversation\. In this case, a [Customer queue flow](create-contact-flow.md#contact-flow-types) is played to customer while they waiting in queue for an agent\.
+ When the available agent accepts the call, an [Agent whisper flow](create-contact-flow.md#contact-flow-types) is played to agent\.
+ A [Customer whisper flow](create-contact-flow.md#contact-flow-types) is played to customer\.
+ After both whisper flows are playedd successfully to the agent and customer respectively, the caller is connected to agent for interaction\.

To summarize API initiation methods, the following contact flows are played before the customer is connected to agent:
+ **Inbound contact flow**
+ **Customer queue flow**
+ **Agent whisper flow**
+ **Customer whisper flow**

## Queue\_Transfer<a name="queue-transfer-initiation-method"></a>

While the customer was in one queue \(listening to a [Customer queue flow](create-contact-flow.md#contact-flow-types)\), they were transferred into another queue using a contact flow block\.
+ The customer who is waiting in the queue for an agent is presented only with a [Customer queue flow](create-contact-flow.md#contact-flow-types)\. No additional flows are involved\.

## Disconnect<a name="disconnect-initiation-method"></a>

When a [Set disconnect flow](set-disconnect-flow.md) block runs, it specifies which contact flow to run after a disconnect event during a contact\.
+ You can specify only an [Inbound contact flow](create-contact-flow.md#contact-flow-types) in this block\. Since it occurs after the disconnect event, no additional flow is presented to customer\.

## Override the default contact flows<a name="override-default-contact-flows"></a>

For all of the initiation methods discussed in this topic, if you don't specify contact flows for **Agent whisper flow**, **Customer whisper flow**, **Customer queue flow**, or **Outbound whisper flow**, then the default contact flow of that type runs instead\. For a list of default contact flows, see [Default contact flows](contact-flow-default.md)\.

To override the defaults and use your own contact flows, use the following blocks:
+ [Set customer queue flow](set-customer-queue-flow.md)
+ [Set hold flow](set-hold-flow.md)
+ [Set whisper flow](set-whisper-flow.md)

For more information, see [Default contact flows](contact-flow-default.md)\. 