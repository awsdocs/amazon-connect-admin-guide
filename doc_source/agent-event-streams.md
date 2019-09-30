# Amazon Connect Agent Event Streams<a name="agent-event-streams"></a>

Amazon Connect agent event streams are Amazon Kinesis data streams that provide you with near real\-time reporting of agent activity within your Amazon Connect instance\. The events published to the stream include these CCP events: 
+ Agent login
+ Agent logout
+ Agent connects with a contact
+ Agent status change, such as to Available to handle contacts, or on Break or at Training\. 

You can use the agent event streams to create dashboards that display agent information and events, integrate streams into workforce management \(WFM\) solutions, and configure alerting tools to trigger custom notifications of specific agent activity\. Agent event streams help you manage agent staffing and efficiency\.

## Enabling Agent Event Streams<a name="agent-event-streams-enable"></a>

Agent event streams are not enabled by default\. Before you can enable agent event streams in Amazon Connect, create a data stream in Amazon Kinesis Data Streams\. Then, choose the Kinesis stream as the stream to use for agent event streams\. Though you can use the same stream for both agent event streams and contact trace records, managing and getting data from the stream is much easier when you use a separate stream for each\. For more information, see the [Amazon Kinesis Data Streams Developer Guide](https://docs.aws.amazon.com/streams/latest/dev/)\.

When data is sent to Kinesis, the partition key used is the agent ARN\. All events for a single agent are sent to the same shard, and any resharding events in the stream are ignored\.

**Note**  
If you enable server\-side encryption for the Kinesis stream you select for agent event streams, Amazon Connect cannot publish to the stream\. This is because it does not have permission to Kinesis `kms:GenerateDataKey`\. To work around this, first enable encryption for scheduled reports or recordings of conversations\. Next, create a customer master key \(CMK\) using KMS for encryption\. Finally, choose the same CMK for your Kinesis data stream that you use for encryption of scheduled reports or recordings of conversations so that Amazon Connect has appropriate permissions to encrypt data sent to Kinesis\. For more information about creating a customer master key \(CMK\) KMS key, see [Creating Keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

**To enable agent event streams**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the console, choose the name in the **Instance Alias** column of the instance for which to enable agent event streams\.

1. Choose **Data streaming**, then select **Enable data streaming**\.

1. Under **Agent Events**, select the Kinesis stream to use, and then choose **Save**\.

## Determine How Long an Agent Spends Doing ACW<a name="determine-acw-time"></a>

There's no event in the agent event stream that tells you how long a contact is in the ACW state, and by extension how long an agent spends doing ACW\. However, there's other data in the agent event stream that you can use to figure this out\. 

First, identify when the contact entered ACW\. Here's how to do that: 

1. Identify when the conversation between the contact and agent `ENDED`\.

1. View the `StateStartTimeStamp` for the event\.

For example, in the following agent event stream output, the contact enters ACW state at "**StateStartTimestamp**": "2019\-05\-25T18:55:27\.017Z"\.

**Tip**  
In the agent event stream, events are listed in reverse chronological order\. We recommend reading through following examples by starting at the bottom of each example\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",  //This just refers to the status that the agent sets manually in the CCP. 
                It means they are ready to handle contacts, not say, on Break.  
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": [
            {
                "Channel": "VOICE",
                "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
                "ContactId": "ContactId-1",  //This is the same contact the agent was working on when their state was CONNECTED (below). 
                    Since it's still the same contact but they aren't connected, we know the contact is now in ACW state.
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",  //This indicates how the contact was initiated. OUTBOUND means the agent initiated contact with the customer. 
                    INBOUND means the customer initiated contact with your center.
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "ENDED",  //This shows the conversation has ended. 
                "StateStartTimestamp": "2019-05-25T18:55:27.017Z"  //This is the timestamp for the ENDED event (above), 
                    which is when the contact entered ACW state.
            }
        ]
    },
    "EventId": "EventId-1",
    "EventTimestamp": "2019-05-25T18:55:27.017Z",
    "EventType": "STATE_CHANGE",  //This shows that the state of the contact has changed; above we can see the conversation ENDED. 
    "InstanceARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available", //This just refers to the status that the agent sets manually in the CCP. 
                It means they were ready to handle contacts, not say, on Break.  
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": [
            {
                "Channel": "VOICE",  //This shows the agent and contact were talking on the phone. 
                "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
                "ContactId": "ContactId-1",  //This shows the agent was working with a contact identified as "ContactId-1".
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "CONNECTED",  //This shows the contact was CONNECTED to the agent, instead of say, MISSED. 
                "StateStartTimestamp": "2019-05-25T18:55:21.011Z"  //This shows when the contact was connected to the agent.
            }
        ]
    },
    "Version": "2019-05-25"
}
```

Next, determine when a contact left ACW\. Here's how to do that: 

1. Find where the `CurrentAgentSnapshot` has no contacts, and the state for the contact listed in the `PreviousAgentSnapshot` equals ENDED\.

   Because a STATE\_CHANGE event also occurs when the agent's configuration is changed, such as when they are assigned a different routing profile, this step confirms you have the right event\.

1. Find where the `EventType` = "STATE\_CHANGE"\.

1. View the `EventTimeStamp` for it\.

For example, in the following agent event stream file, the contact left ACW at "**EventTimestamp**": "2019\-05\-25T18:55:32\.022Z"\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",  //This just refers to the status that the agent sets manually in the CCP. It means they 
                are ready to handle contacts, not say, on Break. 
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": []  //Since a contact isn't listed here, it means ACW for ContactId-1 (below)
            is finished, and the agent is ready for a new contact to be routed to them. 
    },
    "EventId": "477f2c4f-cd1a-4785-b1a8-97023dc1229d",
    "EventTimestamp": "2019-05-25T18:55:32.022Z",  //Here's the EventTimestamp for the STATE_CHANGE event. This is when
        the contact left ACW.
    "EventType": "STATE_CHANGE",  //Here's the STATE_CHANGE
    "InstanceARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",  //This just refers to the status that the agent sets manually in the CCP. 
                It means they were at work, not say, on Break. 
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": [
            {
                "Channel": "VOICE",
                "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
                "ContactId": "ContactId-1",  //This is the ContactId of the customer the agent was working on previously. 
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "ENDED", //The ACW for ContactId-1 has ended.  
                "StateStartTimestamp": "2019-05-25T18:55:27.017Z"
            }
        ]
    },
    "Version": "2019-05-25"
}
```

Finally, to calculate the amount of time the contact was in the ACW state, and thus how long the agent spent working on it:
+ Subtract the "**StateStartTimestamp**": "2019\-05\-25T18:55:27\.017Z" from the "**EventTimestamp**": "2019\-05\-25T18:55:32\.022Z"\. 

In this example, the agent spent 5\.005 seconds doing ACW for ContactId\-1\. 

## Agent Event Streams Data Model<a name="agent-event-stream-model"></a>

Agent event streams are created in JavaScript Object Notation \(JSON\) format\. For each event type, a JSON blob is sent to the Kinesis data stream\. The following event types are included in agent event streams:
+ LOGIN—An agent login to the contact center\.
+ LOGOUT—An agent logout from the contact center\.
+ STATE\_CHANGE—One of the following changed:
  + Something in the agent's configuration changed, such as their routing profile\.
  + The agent changed their status in the CCP\. For example, they changed it from Available to on Break\.
  + The state of the conversation between then agent and contact changed\. For example, they were connected and then on hold\. 
+ HEART\_BEAT—This event is published every 120 seconds if there are no other events published during that interval\.

**Topics**
+ [AgentEvent](#AgentEvent)
+ [AgentSnapshot](#AgentSnapshot)
+ [Configuration](#Configuration)
+ [Contact Object](#Contact)
+ [HierarchyGroup Object](#Hierarchygroup-object)
+ [AgentHierarchyGroups Object](#Hierarchygroups-object)
+ [Queue Object](#queue-object)
+ [RoutingProfile Object](#routingprofile)

### AgentEvent<a name="AgentEvent"></a>

The `AgentEvent` object includes the following properties:

**AgentARN**  
The Amazon Resource Name \(ARN\) for the agent account\.  
Type: ARN

**AWSAccountId**  
The 12\-digit AWS account ID for the AWS account associated with the Amazon Connect instance\.  
Type: String

**CurrentAgentSnapshot**  
Contains agent configuration, such as username, first name, last name, routing profile, hierarchy groups, contacts, and agent status\.  
Type: `AgentSnapshot` object

**EventId**  
Universally unique identifier \(UUID\) for the event\.  
Type: String

**EventTimestamp**  
A time stamp for the event, in ISO 8601 standard format\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*:*sss*Z\)

**EventType**  
The type of event\.   
Valid values: `STATE_CHANGE` \| `HEART_BEAT` \| `LOGIN` \| `LOGOUT` 

**InstanceARN**  
Amazon Resource Name for the Amazon Connect instance in which the agent’s user account is created\.  
Type: ARN

**PreviousAgentSnapshot**  
Contains agent configuration, such as username, first name, last name, routing profile, hierarchy groups\), contacts, and agent status\. Not applicable to LOGIN or LOGOUT events\.  
Type: `AgentSnapshot` object

**Version**  
The version of the agent event stream in date format, such as 2019\-05\-25\.  
Type: String

### AgentSnapshot<a name="AgentSnapshot"></a>

The `AgentSnapshot` object includes the following properties:

**AgentStatus**  
Agent status data, including:  
+ AgentARN—the ARN for the agent\.
+ Name—this is the status of the agent that they manually set in the CCP\. For example, their status might be **Available**, which means that they are ready for inbound contacts to be routed to them\. Or it might be a custom status, such as Break or Training, which means that inbound contacts can't be routed to them BUT they can still make outbound calls\.
+ StartTimestamp—The time stamp in ISO 8601 standard format for the time at which the agent entered the status\.

  Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*:*sss*Z\)
Type: `AgentStatus` object\.

**Configuration**  
Information about the agent, including:   
+ FirstName—The agent's first name\.
+ HierarchyGroups—The hierarchy group the agent is assigned to, if any\.
+ LastName—The agent's last name\.
+ RoutingProfile—The routing profile the agent is assigned to\.
+ Username—the agent's Amazon Connect user name\.
Type: `Configuration` object

**Contacts**  
The contacts  
Type: `ContactList` object

### Configuration<a name="Configuration"></a>

The `Configuration` object includes the following properties:

**FirstName**  
The first name entered in the agent's Amazon Connect account\.  
Type: String  
Length: 1\-100

**AgentHierarchyGroups**  
The hierarchy group, up to five levels of grouping, for the agent associated with the event\.  
Type: `AgentHierarchyGroups` object

**LastName**  
The last name entered in the agent's Amazon Connect account\.  
Type: String  
Length: 1\-100

**RoutingProfile**  
The routing profile assigned to the agent associated with the event\.  
Type: `RoutingProfile` object\.

**Username**  
The user name for the agent's Amazon Connect user account\.  
Type: String  
Length: 1\-100

### Contact Object<a name="Contact"></a>

The `Contact` object includes the following properties:

**ContactId**  
The identifier for the contact\.  
Type: String  
Length: 1\-256

**InitialContactId**  
The original identifier of the contact that was transferred\.  
Type: String  
Length: 1\-256

**Channel**  
The method of communication\.  
Valid values: `VOICE`

**InitiationMethod**  
Indicates how the contact was initiated\.  
Valid values: `INBOUND` \| `OUTBOUND` \| `TRANSFER` \| `CALLBACK` \| `QUEUE_TRANSFER` \| `API`

**State**  
The state of the contact\.  
Valid values: `INCOMING` \| `PENDING` \| `CONNECTING` \| `CONNECTED` \| `CONNECTED_ONHOLD` \| `MISSED` \| `ERROR` \| `ENDED` 

**StateStartTimestamp**  
The time at which the contact entered the current state\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*:*sss*Z\)

**ConnectedToAgentTimestamp**  
The time at which the contact was connected to an agent\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*:*sss*Z\)

**QueueTimestamp**  
The time at which the contact was put into a queue\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*:*sss*Z\)

**Queue**  
The queue the contact was placed in\.  
Type: `Queue` object

### HierarchyGroup Object<a name="Hierarchygroup-object"></a>

The `HierarchyGroup` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the agent hierarchy\.  
Type: String

**Name**  
The name of the hierarchy group\.  
Type: String

### AgentHierarchyGroups Object<a name="Hierarchygroups-object"></a>

The `AgentHierarchyGroups` object includes the following properties:

**Level1**  
Includes details for Level1 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level2**  
Includes details for Level2 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level3**  
Includes details for Level3 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` ob4ject

**Level4**  
Includes details for Level4 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level5**  
Includes details for Level5 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

### Queue Object<a name="queue-object"></a>

The `Queue` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the queue\.  
Type: String

**Name**  
The name of the queue\.  
Type: String

### RoutingProfile Object<a name="routingprofile"></a>

The `RoutingProfile` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the agent's routing profile\.  
Type: String

**Name**  
The name of the routing profile\.  
Type: String

**InboundQueues**  
Thef `Queue` objects associated with the agent's routing profile\.  
Type: List of `Queue` object

**DefaultOutboundQueue**  
The default outbound queue for the agent's routing profile\.  
Type: `Queue` object