# Amazon Connect Agent Event Streams<a name="agent-event-streams"></a>

Amazon Connect agent event streams are Amazon Kinesis data streams that provide you with near real\-time reporting of agent activity within your Amazon Connect instance\. The events published to the stream include agent login, agent logout, agent answers a call, and agent status change\.

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

## Use Agent Event Streams to Determine Agent ACW Time<a name="determine-acw-time"></a>

You can use agent event stream data to determine the amount of time an agent spent in ACW\. Though there is no event in the event stream for the agent entering ACW status, you can use the other agent event data to calculate the time\.

In agent event streams, you can determine the time at which an agent entered ACW status by viewing the `StateStartTimeStamp` for the event for a contact entering the `ENDED` state in the event stream\.

For example, in the following example agent event stream output, the agent enters ACW at "**StateStartTimestamp**": "2018\-10\-25T18:55:27\.027Z"\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",
            "StartTimestamp": "2018-10-25T18:43:59.059Z"
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
                "ConnectedToAgentTimestamp": "2018-10-25T18:55:21.021Z",
                "ContactId": "ContactId-1",
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "ENDED",
                "StateStartTimestamp": "2018-10-25T18:55:27.027Z"  //Agent entered ACW at this time
            }
        ]
    },
    "EventId": "EventId-1",
    "EventTimestamp": "2018-10-25T18:55:27.027Z",
    "EventType": "STATE_CHANGE",
    "InstanceARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",
            "StartTimestamp": "2018-10-25T18:43:59.059Z"
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
                "ConnectedToAgentTimestamp": "2018-10-25T18:55:21.021Z",
                "ContactId": "ContactId-1",
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "CONNECTED",
                "StateStartTimestamp": "2018-10-25T18:55:21.021Z"
            }
        ]
    },
    "Version": "2017-10-01"
}
```

Agent ACW state ends when the agent enters another state, such as when the agent chooses a status in the CCP\. To determine the time at which an agent left ACW status, you can view the `EventTimeStamp` for the `EventType` "STATE\_CHANGE" in the stream output\. Note that a STATE\_CHANGE event also occurs when the agent's configuration is changed, such as the routing profile assigned to the agent\. To confirm that you are using the correct `EventTimeStamp` associated with the agent leaving ACW status, use the `EventTimeStamp` for the event where the associated `CurrentAgentSnapshot` has no contacts listed, and the state for the contact listed in the `PreviousAgentSnapshot` equals ENDED\.

For example, in the following example agent event stream file, the agent left ACW at "**EventTimestamp**": "2018\-10\-25T18:55:32\.032Z"\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",
            "StartTimestamp": "2018-10-25T18:43:59.059Z"
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
        "Contacts": []
    },
    "EventId": "477f2c4f-cd1a-4785-b1a8-97023dc1229d",
    "EventTimestamp": "2018-10-25T18:55:32.032Z",
    "EventType": "STATE_CHANGE",
    "InstanceARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",
            "StartTimestamp": "2018-10-25T18:43:59.059Z"
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
                "ConnectedToAgentTimestamp": "2018-10-25T18:55:21.021Z",
                "ContactId": "ContactId-1",
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "ENDED",
                "StateStartTimestamp": "2018-10-25T18:55:27.027Z"
            }
        ]
    },
    "Version": "2017-10-01"
}
```

To calculate the amount of time an agent spent in ACW, subtract the "**StateStartTimestamp**": "2018\-10\-25T18:55:27\.027Z" from the "**EventTimestamp**": "2018\-10\-25T18:55:32\.032Z"\. In this example, the value is 5\.005 seconds\.

## Agent Event Streams Data Model<a name="agent-event-stream-model"></a>

Agent event streams are created in JavaScript Object Notation \(JSON\) format\. For each event type, a JSON blob is sent to the Kinesis data stream\. The following event types are included in agent event streams:
+ LOGIN—An agent login to the contact center\.
+ LOGOUT—An agent logout from the contact center\.
+ STATE\_CHANGE—One of the following changed:
  + Agent configuration, such as profile or the assigned hierarchy group\.
  + Agent state in the contact control panel, such as Available\.
  + Agent conversation state, such as on hold\.
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
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

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
The version of the agent event stream in date format, such as 2017\-10\-10\.  
Type: String

### AgentSnapshot<a name="AgentSnapshot"></a>

The `AgentSnapshot` object includes the following properties:

**AgentStatus**  
Agent status data, including:  
+ AgentARN—the ARN for the agent\.
+ Name—the name of the status, such as Available or Offline\.
+ StartTimestamp—The time stamp in ISO 8601 standard format for the time at which the agent entered the status\.

  Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)
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
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**ConnectedToAgentTimestamp**  
The time at which the contact was connected to an agent\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**QueueTimestamp**  
The time at which the contact was put into a queue\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

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