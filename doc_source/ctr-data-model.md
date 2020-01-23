# Contact Trace Records Data Model<a name="ctr-data-model"></a>

This article describes the data model for Amazon Connect contact trace records \(CTRs\)\. CTRs capture the events associated with a contact in your contact center\. Real\-time and historical metrics are based on the data captured in the CTRs\.

**Tip**  
Amazon Connect delivers CTRs at least once\. CTRs may be delivered again for multiple reasons, such as new information arriving after initial delivery\. If you're building a system that consumes CTR export streams, be sure to include logic that checks for duplicate CTRs for a contact\. Use the **LastUpdateTimestamp** property to determine if a copy contains new data than previous copies\. Then use the **ContactId** property for deduplication\. 

## Agent<a name="ctr-Agent"></a>

Information about the agent that handled the contact\.

**AgentInteractionDuration**  <a name="AgentInteractionDuration-CTR"></a>
The time, in whole seconds, that an agent interacted with a customer\.  
Type: Integer  
Min value: 0

**AfterContactWorkDuration**  <a name="AfterContactWorkDuration-CTR"></a>
The difference in time, in whole seconds, between `AfterContactWorkStartTimestamp` and `AfterContactWorkEndTimestamp`\.  
Type: Integer  
Min value: 0

**AfterContactWorkEndTimestamp**  
The date and time when the agent stopped doing After Contact Work for the contact, in UTC time\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**AfterContactWorkStartTimestamp**  
The date and time when the agent started doing After Contact Work for the contact, in UTC time\.   
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**ARN**  
The Amazon Resource Name of the agent\.  
Type: ARN

**ConnectedToAgentTimestamp**  
The date and time the contact was connected to the agent, in UTC time\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**CustomerHoldDuration**  <a name="CustomerHoldDuration-CTR"></a>
The time, in whole seconds, that the customer spent on hold while connected to the agent\.  
Type: Integer  
Min value: 0

**HierarchyGroups**  
The agent hierarchy groups for the agent\.  
Type: [AgentHierarchyGroups](#ctr-AgentHierarchyGroups)

**LongestHoldDuration**  
The longest time, in whole seconds, that the customer was put on hold by the agent\.  
Type: Integer  
Min value: 0

**NumberOfHolds**  
The number of times the customer was put on hold while connected to the agent\.  
Type: Integer  
Min value: 0

**RoutingProfile**  
The routing profile of the agent\.  
Type: [RoutingProfile](#ctr-RoutingProfile)

**Username**  
The username of the agent\.  
Type: String  
Length: 1\-100

## AgentHierarchyGroup<a name="ctr-AgentHierarchyGroup"></a>

Information about an agent hierarchy group\.

**ARN**  
The Amazon Resource Name \(ARN\) of the group\.  
Type: ARN

**GroupName**  
The name of the hierarchy group\.  
Type: String  
Length: 1\-256

## AgentHierarchyGroups<a name="ctr-AgentHierarchyGroups"></a>

Information about the agent hierarchy\. Hierarchies can be configured with up to five levels\.

**Level1**  
The group at level one of the agent hierarchy\.  
Type: [AgentHierarchyGroup](#ctr-AgentHierarchyGroup)

**Level2**  
The group at level two of the agent hierarchy\.  
Type: [AgentHierarchyGroup](#ctr-AgentHierarchyGroup)

**Level3**  
The group at level three of the agent hierarchy\.  
Type: [AgentHierarchyGroup](#ctr-AgentHierarchyGroup)

**Level4**  
The group at level four of the agent hierarchy\.  
Type: [AgentHierarchyGroup](#ctr-AgentHierarchyGroup)

**Level5**  
The group at level five of the agent hierarchy\.  
Type: [AgentHierarchyGroup](#ctr-AgentHierarchyGroup)

## ContactTraceRecord<a name="ctr-ContactTraceRecord"></a>

Information about a contact\.

**Agent**  
If this contact successfully connected to an agent, this is information about the agent\.  
Type: [Agent](#ctr-Agent)

**AgentConnectionAttempts**  
The number of times Amazon Connect attempted to connect this contact with an agent\.  
Type: Integer  
Min value: 0

**Attributes**  
The contact attributes, formatted as a map of keys and values\.  
Type: Attributes  
Members: `AttributeName`, `AttributeValue` 

**AWSAccountId**  
The ID of the AWS account that owns the contact\.  
Type: String

**AWSContactTraceRecordFormatVersion**  
The record format version\.  
Type: String

**Channel**  
How the customer reached your contact center\.  
Valid values: Voice, Chat

**ConnectedToSystemTimestamp**  
The date and time the customer endpoint connected to Amazon Connect, in UTC time\. For `INBOUND`, this matches `InitiationTimestamp`\. For `OUTBOUND`, `CALLBACK`, and `API`, this is when the customer endpoint answers\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**ContactId**  
The ID of the contact\.  
Type: String  
Length: 1\-256

**CustomerEndpoint**  
The customer endpoint\.  
Type: [Endpoint](#ctr-endpoint)

**DisconnectTimestamp**  
The date and time that the customer endpoint disconnected from Amazon Connect, in UTC time\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**InitialContactId**  
If this contact is related to other contacts, this is the ID of the initial contact\.  
Type: String  
Length: 1\-256

**InitiationMethod**  
Indicates how the contact was initiated\.  
Valid values: `INBOUND` \| `OUTBOUND` \| `TRANSFER` \| `CALLBACK` \| `API` \| `QUEUE_TRANSFER` 

**InitiationTimestamp**  
The date and time this contact was initiated, in UTC time\. For `INBOUND`, this is when the contact arrived\. For `OUTBOUND`, this is when the agent began dialing\. For `CALLBACK`, this is when the callback contact was created\. For `TRANSFER` and `QUEUE_TRANSFER`, this is when the transfer was initiated\. For `API`, this is when the request arrived\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**InstanceARN**  
The Amazon Resource Name of the Amazon Connect instance\.  
Type: ARN

**LastUpdateTimestamp**  
The date and time this contact was last updated, in UTC time\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**MediaStreams**  
The media streams\.  
Type: Array of [MediaStream](#MediaStream)

**NextContactId**  
If this contact is not the last contact, this is the ID of the next contact\.  
Type: String  
Length: 1\-256

**PreviousContactId**  
If this contact is not the first contact, this is the ID of the previous contact\.  
Type: String  
Length: 1\-256

**Queue**  
If this contact was queued, this is information about the queue\.  
Type: [QueueInfo](#ctr-QueueInfo)

**Recording**  
If recording was enabled, this is information about the recording\.  
Type: [RecordingInfo](#ctr-RecordingInfo)

**Recordings**  
If recording was enabled, this is information about the recording\.  
Type: [RecordingInfo](#ctr-RecordingInfo)  
The first recording for a contact will appear in both the Recording and Recordings sections of the CTR\.

**SystemEndpoint**  
The system endpoint\. For `INBOUND`, this is the phone number that the customer dialed\. For `OUTBOUND`, this is the caller ID phone number that Amazon Connect used to dial the customer\.  
Type: [Endpoint](#ctr-endpoint)

**TransferCompletedTimestamp**  
If this contact was transferred out of Amazon Connect, the date and time the transfer endpoint was connected, in UTC time\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**TransferredToEndpoint**  
If this contact was transferred out of Amazon Connect, the transfer endpoint\.  
Type: [Endpoint](#ctr-endpoint)

## Endpoint<a name="ctr-endpoint"></a>

Information about an endpoint\. In Amazon Connect, an endpoint is the destination for a contact, such as a customer phone number, or a phone number for your contact center\.

**Address**  
The value for the type of endpoint\. For TELEPHONE\_NUMBER, the value is a phone number in E\.164 format\.  
Type: String  
Length: 1\-256

**Type**  
The endpoint type\. Currently, an endpoint can only be a telephone number\.  
Valid values: `TELEPHONE_NUMBER` 

## MediaStream<a name="MediaStream"></a>

Information about the media stream used on the contact\.

**Type**  
Type: MediaStreamType  
Valid value: AUDIO

## QueueInfo<a name="ctr-QueueInfo"></a>

Information about a queue\.

**ARN**  
The Amazon Resource Name of the queue\.  
Type: ARN

**DequeueTimestamp**  <a name="DequeueTimestamp-CTR"></a>
The date and time the contact was removed from the queue, in UTC time\. Either the customer disconnected or the contact was connected to an agent\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**Duration**  <a name="Duration-CTR"></a>
The difference in time, in whole seconds, between `EnqueueTimestamp` and `DequeueTimestamp`\.  
Type: Integer  
Min value: 0

**EnqueueTimestamp**  <a name="EnqueueTimestamp-CTR"></a>
The date and time the contact was added to the queue, in UTC time\.  
Type: String \(*yyyy*\-*mm*\-*dd*T*hh*:*mm*:*ss*Z\)

**Name**  
The name of the queue\.  
Type: String  
Length: 1\-256

## RecordingInfo<a name="ctr-RecordingInfo"></a>

Information about a recording\.

**DeletionReason**  
If the recording was deleted, this is the reason entered for the deletion\.  
Type: String

**Location**  
The location, in Amazon S3, for the recording\.  
Type: String  
Length: 0\-256

**Status**  
The recording status\.  
Valid values: `AVAILABLE` \| `DELETED` \| `NULL` 

**Type**  
The recording type\.  
Valid values: `AUDIO` 

## RoutingProfile<a name="ctr-RoutingProfile"></a>

Information about a routing profile\.

**ARN**  
The Amazon Resource Name of the routing profile\.  
Type: ARN

**Name**  
The name of the routing profile\.  
Type: String  
Length: 1\-100

## How to Identify Abandoned Contacts<a name="abandoned-contact"></a>

An abandoned contact refers to a contact that was disconnected by the customer while in queue\. This means that they weren't connected to an agent\. 

The CTR for an abandoned contact has a **Queue**, and an **Enqueue Timestamp** because it was enqueued\. It won’t have a **ConnectedToAgentTimestamp**, or any of the other fields that populate only after the contact has been connected to an agent\.