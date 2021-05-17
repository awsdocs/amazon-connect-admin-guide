# Amazon Connect contact events<a name="contact-events"></a>

Amazon Connect allows you to subscribe to a near real\-time stream of contact \(voice calls, chat, and task\) events \(for example, call is queued\) in your Amazon Connect contact center\. These events include:
+ INITIATED \- A voice call, chat, or task is initiated or transferred\. 
+ QUEUED \- A voice call, chat, or task is queued to be assigned to an agent\.
+ CONNECTED\_TO\_AGENT \- A voice call, chat, or task is connected to an agent\.
+ DISCONNECTED \- A voice call, chat, or task is disconnected\. 

You can use contact events to create analytics dashboards to monitor and track contact activity, integrate into workforce management \(WFM\) solutions to better understand contact center performance, or to integrate applications that react to events \(for example, call disconnected\) in real\-time\. 

## Subscribe to Amazon Connect contact events<a name="subscribe-contact-events"></a>

Amazon Connect contact events are published using [Amazon EventBridge](http://aws.amazon.com/eventbridge/), and can be enabled in a couple of steps for your Amazon Connect instance in the Amazon EventBridge console by creating a new rule\. Although events are not ordered, they have a timestamp which enables you to consume the data\.

To subscribe to Amazon Connect contact events, go to Amazon EventBridge and create a new rule by selecting **Amazon Connect** as the service name, and **Amazon Connect contact event** as the event type\. For more information about configuring rules, see [Amazon EventBridge rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-rules.html) in the *Amazon EventBridge User Guide*\. 

The following image shows what this looks like in EventBridge:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-events-eventbridge-rule.png)

You can then select a target of your choice which includes a Lambda function, SQS queue, or SNS topic\. For information about configuring targets, [Amazon EventBridge targets](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-targets.html)\. 

## Contact events data model<a name="contact-events-data-model"></a>

Contact events are generated in JSON\. For each event type, a JSON blob is sent to the target of your choice, as configured in the rule\. The following contact events are available: 
+ INITIATED \- A voice call, chat, or task is initiated or transferred\. 
+ QUEUED \- A voice call, chat, or task is queued to be assigned to an agent\.
+ CONNECTED\_TO\_AGENT \- A voice call, chat, or task is connected to an agent\.
+ DISCONNECTED \- A voice call, chat, or task is disconnected\. 

**Topics**
+ [Contact event](#ContactEvent)
+ [QueueInfo](#QueueInfo)
+ [AgentInfo](#AgentInfo)

### Contact event<a name="ContactEvent"></a>

The `Contact` object includes the following properties:

**EventType**  
The type of event published\.  
Type: String  
Valid values: INITIATED, QUEUED, CONNECTED\_TO\_AGENT, DISCONNECTED

**ContactId**  
The identifier for the contact\.  
Type: String  
Length: 1\-256

**InitialContactId**  
The original identifier of the contact that was transferred\.  
Type: String  
Length: 1\-256

**PreviousContactId**  
The original identifier of the contact that was transferred\.  
Type: String  
Length: 1\-256

**InstanceARN**  
Amazon Resource Name for the Amazon Connect instance in which the agent's user account is created\.  
Type: ARN

**Channel**  
The type of channel\.  
Type: `VOICE`, `CHAT`, or `TASK`

**QueueInfo**  
The queue the contact was placed in\.  
Type: `QueueInfo` object 

**AgentInfo**  
The agent the contact was assigned to\.  
Type: `AgentInfo` object 

**InitiationMethod**  
Indicates how the contact was initiated\.  
Valid values:  
+ INBOUND: The customer initiated voice \(phone\) contact with your contact center\.
+ OUTBOUND: An agent initiated voice \(phone\) contact with the customer, by using the CCP to call their number\. This initiation method calls the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API\.
+ TRANSFER: The contact was transferred by an agent to another agent or to a queue, using quick connects in the CCP\. This results in a new CTR being created\.
+ CALLBACK: The customer was contacted as part of a callback flow\. For more information about the InitiationMethod in this scenario, see [About queued callbacks in metrics](about-queued-callbacks.md)\. 
+ API: The contact was initiated with Amazon Connect by API\. This could be an outbound contact you created and queued to an agent, using the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API, or it could be a live chat that was initiated by the customer with your contact center, where you called the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API, or it could be a tasks initiated by the customer by calling the [StartTaskContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API\. 
+ QUEUE\_TRANSFER: While the contact is one queue, and was then transferred into another queue using a contact flow block\.
+ DISCONNECT: When a [Set disconnect flow](set-disconnect-flow.md) block is triggered, it specifies which contact flow to run after a disconnect event\. A disconnect event is when an agent disconnects\. When the disconnect event occurs, the corresponding content flow runs\. If a new contact is created while running a disconnect flow, then the initiation method for that new contact is DISCONNECT\.

### QueueInfo<a name="QueueInfo"></a>

The `QueueInfo` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the queue\.  
Type: String

**QueueType**  
The type of queue\.  
Type: String

### AgentInfo<a name="AgentInfo"></a>

The `AgentInfo` object includes the following properties:

**AgentARN**  
The Amazon Resource Name \(ARN\) for the agent account\.  
Type: ARN

**RoutingProfileArn**  
The Amazon Resource Name \(ARN\) for the agent's routing profile\.  
Type: String

## Sample contact event for when a voice call is connected to an agent<a name="sample-contact-event"></a>

```
{
"version": "0", 
"id": "abcabcab-abca-abca-abca-abcabcabcabc", 
"detail-type": "Amazon Connect Contact Event", 
"source": "aws.connect", 
"account": "111122223333", 
"time": "2021-05-01T18:43:48Z",   // this is the timestamp
"region": "us-west-1", 
"resources": [ "arn:aws..." contactArn and instanceArn
],
"detail": { 
    "EventType": "CONNECTED_TO_AGENT", 
    "ContactId": "11111111-1111-1111-1111-111111111111",
    "InitialContactId": "11111111-2222-3333-4444-555555555555",
    "PreviousContactId": "11111111-2222-3333-4444-555555555555",
    "Channel": "Voice",
    "InstanceARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012",
    "InitiationMethod": "INBOUND",
    "QueueInfo": {
        "QueueArn": "arn",       
        "QueueType": "type"
},
"AgentInfo": {
    "AgentArn" : "arn"
            "RoutingProfileArn": "",
     }
}
```