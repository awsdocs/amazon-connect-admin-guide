# Agent event streams data model<a name="agent-event-stream-model"></a>

Agent event streams are created in JavaScript Object Notation \(JSON\) format\. For each event type, a JSON blob is sent to the Kinesis data stream\. The following event types are included in agent event streams:
+ LOGIN—An agent login to the contact center\.
+ LOGOUT—An agent logout from the contact center\.
+ STATE\_CHANGE—One of the following changed:
  + The agent changed their status in the Contact Control Panel \(CCP\)\. For example, they changed it from Available to on Break\.
  + The state of the conversation between the agent and contact changed\. For example, they were connected and then on hold\. 
  + One of the following settings changed in the agent's configuration:
    + Their routing profile
    + The queues in their routing profile
    + Phone type: soft phone or desk phone
    + Auto\-accept call
    + Sip address
    + Agent hierarchy group
    + Language preference setting in the CCP
+ HEART\_BEAT—This event is published every 120 seconds if there are no other events published during that interval\.

**Topics**
+ [AgentEvent](#AgentEvent)
+ [AgentSnapshot](#AgentSnapshot)
+ [Configuration](#Configuration)
+ [Contact object](#Contact)
+ [HierarchyGroup object](#Hierarchygroup-object)
+ [AgentHierarchyGroups object](#Hierarchygroups-object)
+ [Queue object](#queue-object)
+ [RoutingProfile object](#routingprofile)

## AgentEvent<a name="AgentEvent"></a>

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

## AgentSnapshot<a name="AgentSnapshot"></a>

The `AgentSnapshot` object includes the following properties:

**AgentStatus**  
Agent status data, including:  
+ AgentARN—The ARN for the agent\.
+ Name—This is the [status of the agent that they manually set in the CCP](metrics-agent-status.md), or that the supervisor manually [changes in the real\-time metrics report](rtm-change-agent-activity-state.md)\. 

  For example, their status might be **Available**, which means that they are ready for inbound contacts to be routed to them\. Or it might be a custom status, such as Break or Training, which means that inbound contacts can't be routed to them BUT they can still make outbound calls\.
+ StartTimestamp—The timestamp in ISO 8601 standard format for the time at which the agent entered the status\.

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

## Configuration<a name="Configuration"></a>

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

## Contact object<a name="Contact"></a>

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

## HierarchyGroup object<a name="Hierarchygroup-object"></a>

The `HierarchyGroup` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the agent hierarchy\.  
Type: String

**Name**  
The name of the hierarchy group\.  
Type: String

## AgentHierarchyGroups object<a name="Hierarchygroups-object"></a>

The `AgentHierarchyGroups` object includes the following properties:

**Level1**  
Includes details for Level1 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level2**  
Includes details for Level2 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level3**  
Includes details for Level3 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level4**  
Includes details for Level4 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

**Level5**  
Includes details for Level5 of the hierarchy assigned to the agent\.  
Type: `HierarchyGroup` object

## Queue object<a name="queue-object"></a>

The `Queue` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the queue\.  
Type: String

**Name**  
The name of the queue\.  
Type: String

## RoutingProfile object<a name="routingprofile"></a>

The `RoutingProfile` object includes the following properties:

**ARN**  
The Amazon Resource Name \(ARN\) for the agent's routing profile\.  
Type: String

**Name**  
The name of the routing profile\.  
Type: String

**InboundQueues**  
The `Queue` objects associated with the agent's routing profile\.  
Type: List of `Queue` object

**DefaultOutboundQueue**  
The default outbound queue for the agent's routing profile\.  
Type: `Queue` object