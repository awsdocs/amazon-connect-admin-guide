# Amazon Connect contact events<a name="contact-events"></a>

Amazon Connect allows you to subscribe to a near real\-time stream of contact \(voice calls, chat, and task\) events \(for example, call is queued\) in your Amazon Connect contact center\.

You can use contact events to create analytics dashboards to monitor and track contact activity, integrate into workforce management \(WFM\) solutions to better understand contact center performance, or to integrate applications that react to events \(for example, call disconnected\) in real\-time\.

**Topics**
+ [Subscribe to Amazon Connect contact events](#subscribe-contact-events)
+ [Contact events data model](#contact-events-data-model)
+ [Contact timestamps](#contact-timestamps)
+ [Sample contact event for when a voice call is connected to an agent](#sample-contact-event)
+ [Sample contact event for when a voice call is disconnected](#sample-contact-event-call-disconnected)

## Subscribe to Amazon Connect contact events<a name="subscribe-contact-events"></a>

Amazon Connect contact events are published using [Amazon EventBridge](http://aws.amazon.com/eventbridge/), and can be enabled in a couple of steps for your Amazon Connect instance in the Amazon EventBridge console by creating a new rule\. Although events are not ordered, they have a timestamp which enables you to consume the data\.

Events are emitted on a best effort basis\.

To subscribe to Amazon Connect contact events, go to Amazon EventBridge and create a new rule by selecting **Amazon Connect** as the service name, and **Amazon Connect contact event** as the event type\. For more information about configuring rules, see [Amazon EventBridge rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-rules.html) in the *Amazon EventBridge User Guide*\. 

The following image shows what this looks like in EventBridge:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-events-eventbridge-rule.png)

You can then select a target of your choice which includes a Lambda function, SQS queue, or SNS topic\. For information about configuring targets, [Amazon EventBridge targets](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-targets.html)\. 

## Contact events data model<a name="contact-events-data-model"></a>

Contact events are generated in JSON\. For each event type, a JSON blob is sent to the target of your choice, as configured in the rule\. The following contact events are available: 
+ INITIATED \- A voice call, chat, or task is initiated or transferred\. 
+ CONNECTED\_TO\_SYSTEM \- The contact has established media \(for example, was answered by a human or a machine\)\. This event uses the following status codes to identify the actual disposition if the contact was connected to Amazon Connect: `HUMAN_ANSWERED`, `SIT_TONE-DETECTED`, `FAX_MACHINE_DETECTED`, `VOICEMAIL_BEEP`, `VOICEMAIL_NO_BEEP`, `AMD_UNRESOLVED`, `AMD_ERROR`\. 
**Note**  
This event is generated for outbound calls \([Amazon Connect Campaign](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) with answering machine detection enabled\), Tasks, and Chats\.
+ QUEUED \- A voice call, chat, or task is queued to be assigned to an agent\.
+ CONNECTED\_TO\_AGENT \- A voice call, chat, or task is connected to an agent\.
+ DISCONNECTED \- A voice call, chat, or task is disconnected\. For outbound calls, the dial attempt is not successful, the attempt is connected but the call is not picked up, or the attempt results in a [SIT tone](https://en.wikipedia.org/wiki/Special_information_tone)\. 

  A disconnect event is when:
  + A call, chat, or task is disconnected by an agent\.
  + A task is disconnected as a result of a flow action\.
  + A task expires\. The task is automatically disconnected if it is not completed in 7 days\. 

**Topics**
+ [Contact event](#ContactEvent)
+ [QueueInfo](#QueueInfo)
+ [AgentInfo](#AgentInfo)
+ [CustomerVoiceActivity](#CustomerVoiceActivity)

### Contact event<a name="ContactEvent"></a>

The `Contact` object includes the following properties:

**EventType**  
The type of event published\.  
Type: String  
Valid values: INITIATED, CONNECTED\_TO\_SYSTEM, QUEUED, CONNECTED\_TO\_AGENT, DISCONNECTED

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

**InstanceArn**  
Amazon Resource Name \(ARN\) for the Amazon Connect instance in which the agent's user account is created\.  
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
+ OUTBOUND: Represents an agent\-initiated outbound voice call from the Contact Control Panel \(CCP\)\. This initiation method calls the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API\.
+ TRANSFER: The contact was transferred by an agent to another agent or to a queue, using quick connects in the CCP\. This results in a new contact record being created\.
+ CALLBACK: The customer was contacted as part of a callback flow\. For more information about the InitiationMethod in this scenario, see [About queued callbacks in metrics](about-queued-callbacks.md)\. 
+ API: The contact was initiated with Amazon Connect by API\. This could be an outbound contact you created and queued to an agent, using the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API, or it could be a live chat that was initiated by the customer with your contact center, where you called the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API, or it could be a tasks initiated by the customer by calling the [StartTaskContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API\. 
+ QUEUE\_TRANSFER: While the contact is one queue, and was then transferred into another queue using a flow block\.
+ DISCONNECT: When a [Set disconnect flow](set-disconnect-flow.md) block is triggered, it specifies which flow to run after a disconnect event\. 

  A disconnect event is when:
  + A call, chat, or task is disconnected by an agent\.
  + A task is disconnected as a result of a flow action\.
  + A task expires\. The task is automatically disconnected if it is not completed in 7 days\. 

  When the disconnect event occurs, the corresponding content flow runs\. If a new contact is created while running a disconnect flow, then the initiation method for that new contact is DISCONNECT\.

### QueueInfo<a name="QueueInfo"></a>

The `QueueInfo` object includes the following properties:

**QueueArn**  
The Amazon Resource Name \(ARN\) for the queue\.  
Type: String

**QueueType**  
The type of queue\.  
Type: String

### AgentInfo<a name="AgentInfo"></a>

The `AgentInfo` object includes the following properties:

**AgentArn**  
The Amazon Resource Name \(ARN\) for the agent account\.  
Type: ARN

### CustomerVoiceActivity<a name="CustomerVoiceActivity"></a>

The `CustomerVoiceActivity` object includes the following properties:

**GreetingStartTimestamp**  
The date and time that measures the beginning of the customer greeting from an outbound voice call, in UTC time\.   
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\)

**GreetingEndTimestamp**  
The date and time that measures the end of the customer greeting from an outbound voice call, in UTC time\.   
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\)

## Contact timestamps<a name="contact-timestamps"></a>

**InitiationTimestamp**  
The date and time this contact was initiated, in UTC time\.  
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\) 

**ConnectedToSystemTimestamp**  
The date and time the customer endpoint connected to Amazon Connect, in UTC time\.

**EnqueueTimestamp**  
The date and time the contact was added to the queue, in UTC time\.  
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\) 

**ConnectedToAgentTimestamp**  
The date and time the contact was connected to the agent, in UTC time\.  
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\) 

**DisconnectTimestamp**  
The date and time that the customer endpoint disconnected from Amazon Connect, in UTC time  
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\) 

**ScheduledTimestamp**  
The date and time when this contact was scheduled to trigger the flow to run, in UTC time\. This is supported only for the task channel\.  
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\) 

**GreetingStartTimestamp**  
The date and time that measures the beginning of the customer greeting from an outbound voice call, in UTC time\.   
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\)

**GreetingEndTimestamp**  
The date and time that measures the end of the customer greeting from an outbound voice call, in UTC time\.   
Type: String \(yyyy\-MM\-dd'T'HH:mm:ss\.SSS'Z'\)

## Sample contact event for when a voice call is connected to an agent<a name="sample-contact-event"></a>

```
{
"initiationTimestamp":"2021-08-04T17:17:53.000Z",
"contactId":"11111111-1111-1111-1111-111111111111",
"channel":"VOICE",
"instanceArn":"arn:aws::connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012",
"initiationMethod":"INBOUND",
"eventType":"CONNECTED_TO_AGENT",
"agentInfo":{
  "agentArn":"arn:aws::connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent/12345678-1234-1234-1234-123456789012",
  "connectedToAgentTimestamp":"2021-08-04T17:29:09.000Z"
},
"queueInfo": {  
    "queueType":"type",
    "queueArn":"arn:aws::connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/12345678-1234-1234-1234-123456789012",
    "enqueueTimestamp":"2021-08-04T17:29:04.000Z"
  }
}
```

## Sample contact event for when a voice call is disconnected<a name="sample-contact-event-call-disconnected"></a>

```
{
    "version": "0",
    "id": "abcabcab-abca-abca-abca-abcabcabcabc",
    "detail-type": "Amazon Connect Contact Event",
    "source": "aws.connect",
    "account": "111122223333",
    "time": "2021-08-04T17:43:48Z",
    "region": "us-west-1",
    "resources": [
        "arn:aws:...", 
        "contactArn", 
        "instanceArn"
    ],
    "detail": {
        "eventType": "DISCONNECTED",
        "contactId": "11111111-1111-1111-1111-111111111111",
        "initialContactId": "11111111-2222-3333-4444-555555555555",
        "previousContactId": "11111111-2222-3333-4444-555555555555",
        "channel": "Voice",
        "instanceArn": "arn:aws::connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012",
        "initiationMethod": "OUTBOUND",
        "initiationTimestamp":"2021-08-04T17:17:53.000Z",
        "connectedToSystemTimestamp":"2021-08-04T17:17:55.000Z",
        "disconnectTimestamp":"2021-08-04T17:18:37.000Z",
        "queueInfo": {
            "queueArn": "arn",
            "queueType": "type",
            "enqueueTimestamp": "2021-08-04T17:29:04.000Z"
        },
        "AgentInfo": {
            "AgentArn": "arn",
            "connectedToAgentTimestamp":"2021-08-04T17:29:09.000Z"
        },
        "CustomerVoiceActivity": {
           "greetingStartTimestamp":"2021-08-04T17:29:20.000Z",
           "greetingEndTimestamp":"2021-08-04T17:29:22.000Z",
        }
    }
}
```