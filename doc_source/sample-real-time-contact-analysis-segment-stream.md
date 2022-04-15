# Sample real\-time contact analysis segment stream<a name="sample-real-time-contact-analysis-segment-stream"></a>

This topic provides sample segment streams for STARTED, SEGMENTS, COMPLETED, and FAILED events\. 

## Sample STARTED event<a name="sample-started-event"></a>
+ EventType: STARTED
+ Published at the beginning of the real\-time contact analysis session\.

```
{
    "Version": "1.0.0",
    "Channel": "VOICE",
    "AccountId": "your AWS account ID",
    "InstanceId": "your Amazon Connect instance ID",
    "ContactId": "the ID of the contact",
    "LanguageCode": "the language code of the contact",
    "EventType": "STARTED"
}
```

## Sample SEGMENTS event<a name="sample-segments-event"></a>
+ EventType: SEGMENTS
+ Published during a real\-time contact analysis session\. This event contains a list of segments with analyzed information\. The list of segments may include "`Utterance`," "`Transcript`," or "`Categories`" segments\.

```
{
    "Version": "1.0.0",
    "Channel": "VOICE",
    "AccountId": "your AWS account ID",
    "InstanceId": "your Amazon Connect instance ID",
    "ContactId": "the ID of the contact",
    "LanguageCode": "the language code of the contact",
    "EventType": "SEGMENTS",
    "Segments": [
        {
            "Utterance": {
                "Id": "the ID of the utterance",
                "TranscriptId": "the ID of the transcript",
                "ParticipantId": "AGENT",
                "ParticipantRole": "AGENT",
                "PartialContent": "Hello, thank you for calling Example Corp. My name is Adam.",
                "BeginOffsetMillis": 19010,
                "EndOffsetMillis": 22980
            }
        },
        {
            "Utterance": {
                "Id": "the ID of the utterance",
                "TranscriptId": "the ID of the transcript",
                "ParticipantId": "AGENT",
                "ParticipantRole": "AGENT",
                "PartialContent": "How can I help you?",
                "BeginOffsetMillis": 23000,
                "EndOffsetMillis": 24598
            }
        },
        {
            "Transcript": {
                "Id": "the ID of the transcript",
                "ParticipantId": "AGENT",
                "ParticipantRole": "AGENT",
                "Content": "Hello, thank you for calling Example Corp. My name is Adam. How can I help you?",
                "BeginOffsetMillis": 19010,
                "EndOffsetMillis": 24598,
                "Sentiment": "NEUTRAL"
            }
        },
        {
            "Transcript": {
                "Id": "the ID of the transcript",
                "ParticipantId": "CUSTOMER",
                "ParticipantRole": "CUSTOMER",
                "Content": "I'm having trouble submitting the application, number AX876293 on the portal. I tried but couldn't connect to my POC on the portal. So, I'm calling on this toll free number",
                "BeginOffsetMillis": 19010,
                "EndOffsetMillis": 22690,
                "Sentiment": "NEGATIVE",
                "IssuesDetected": [
                    {
                        "CharacterOffsets": {
                            "BeginOffsetChar": 0,
                            "EndOffsetChar": 81
                        }
                    }
                ]
            }
        },
        {
            "Categories": {
                "MatchedCategories": [
                    "CreditCardRelated",
                    "CardBrokenIssue"
                ],
                "MatchedDetails": {
                    "CreditCardRelated": {
                        "PointsOfInterest": [
                            {
                                "BeginOffsetMillis": 19010,
                                "EndOffsetMillis": 22690
                            }
                        ]
                    },
                    "CardBrokenIssue": {
                        "PointsOfInterest": [
                            {
                                "BeginOffsetMillis": 25000,
                                "EndOffsetMillis": 29690
                            }
                        ]
                    }
                }
            }
        }
    ]
}
```

## Sample COMPLETED event<a name="sample-completed-event"></a>
+ EventType: COMPLETED
+ Published at the end of the real\-time contact analysis session if the analysis completed successfully\.

```
{
    "Version": "1.0.0",
    "Channel": "VOICE",
   "AccountId": "your AWS account ID",
    "InstanceId": "your Amazon Connect instance ID",
    "ContactId": "the ID of the contact",
    "LanguageCode": "the language code of the contact",
    "EventType": "COMPLETED"
}
```

## Sample FAILED event<a name="sample-failed-event"></a>
+ EventType: FAILED
+ Published at the end of the real\-time contact analysis session if the analysis failed\.

```
{
    "Version": "1.0.0",
    "Channel": "VOICE",
    "AccountId": "your AWS account ID",
    "InstanceId": "your Amazon Connect instance ID",
    "ContactId": "the ID of the contact",
    "LanguageCode": "the language code of the contact",
    "EventType": "FAILED"
}
```