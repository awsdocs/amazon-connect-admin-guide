# Real\-time contact analysis segment streams data model<a name="real-time-contact-analysis-segment-streams-data-model"></a>

Real\-time contact analysis segment streams are generated in JSON\. Event JSON blobs are published to the associated stream for every contact that has real\-time contact analysis enabled\. The following types of events can be published for a real\-time contact analysis session:
+ STARTED events—Each real\-time contact analysis session publishes one STARTED event at the beginning of the session\.
+ SEGMENTS events—Each real\-time contact analysis session may publish zero or more SEGMENTS events during the session\. These events contain a list of segments with analyzed information\. The list of segments may include "`Utterance`," "`Transcript`," or "`Categories`" segments\.
+ COMPLETED or FAILED events—Each real\-time contact analysis session publishes one COMPLETED or FAILED event at the end of the session\.

## Common properties included in all events<a name="segment-streams-data-model-common-properties"></a>

Every event includes the following properties:

**Version**  
The version of the event schema\.  
Type: String

**Channel**  
The type of channel for this contact\.  
Type: String  
Valid values: `VOICE`, `CHAT`, `TASK`  
For more information about channels, see [Channels and concurrency](channels-and-concurrency.md)\.

**AccountId**  
The identifier of the account where this contact takes place\.  
Type: String

**ContactId**  
The identifier of the contact being analyzed\.  
Type: String

**InstanceId**  
The identifier of the instance where this contact takes place\.  
Type: String 

**LanguageCode**  
The language code associated to this contact\.  
Type: String   
Valid values: the language code for one of the [supported languages for Contact Lens real\-time call analytics](supported-languages.md#supported-languages-contact-lens)\. 

**EventType**  
The type of event published\.  
Type: String  
Valid values: `STARTED`, `SEGMENTS`, `COMPLETED`, `FAILED` 

## STARTED event<a name="segment-streams-data-model-started-event"></a>

`STARTED` events include only the common properties:
+ Version
+ Channel
+ AccountId
+ ContactId
+ LanguageCode
+ EventType: STARTED

## SEGMENTS event<a name="segment-streams-data-model-segments-event"></a>

`SEGMENTS` events include the following properties:
+ Version
+ Channel
+ AccountId
+ ContactId
+ LanguageCode
+ EventType: SEGMENTS
+ Segments: In addition to the common properties, `SEGMENTS` events include a list of segments with analyzed information\.

  Type: Array of [Segment](#segment) objects

**Segment**  
An analyzed segment for a real\-time analysis session\.  
Each segment is an object with the following optional properties\. Only one of these properties is present, depending on the segment type:  
+ Utterance
+ Transcript
+ Categories

**Utterance**  
The analyzed utterance\.  
Required: No  
+ **Id**

  The identifier of the utterance\.

  Type: String
+ ** TranscriptId**

  The identifier of the transcript associated to this utterance\.

  Type: String
+ ** ParticipantId**

  The identifier of the participant\.

  Type: String
+ ** ParticipantRole**

  The role of participant\. For example, is it a customer, agent, or system\.

  Type: String
+ ** PartialContent**

  The content of the utterance\.

  Type: String
+ ** BeginOffsetMillis**

  The beginning offset in the contact for this transcript\.

  Type: Integer
+ ** EndOffsetMillis**

  The end offset in the contact for this transcript\.

  Type: Integer

**Transcript**  
The analyzed transcript\.  
Type: [Transcript](https://docs.aws.amazon.com/contact-lens/latest/APIReference/API_Transcript.html) object   
Required: No

**Categories**  
The matched category rules\.  
Type: [Categories](https://docs.aws.amazon.com/contact-lens/latest/APIReference/API_Categories.html) object  
Required: No

## COMPLETED event<a name="segment-streams-data-model-completed-event"></a>

`COMPLETED` events include only the following common properties:
+ Version
+ Channel
+ AccountId
+ ContactId
+ LanguageCode
+ EventType: STARTED

## FAILED event<a name="segment-streams-data-model-failed-event"></a>

`FAILED` events include only the following common properties:
+ Version
+ Channel
+ AccountId
+ ContactId
+ LanguageCode
+ EventType: FAILED