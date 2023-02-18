# Example Contact Lens output files for a chat<a name="contact-lens-example-output-files-chat"></a>

This section shows an example schema for a chat conversation that Contact Lens has analyzed\. The example shows inferred sentiment, matched categories, contact summary, and response time\.

The original, analyzed file contains the full chat transcript\. The same content that is present in the chat **Transcript** field on the **Contact details** page is present in `Transcript` field in the original Contact Lens analysis file\. In addition, the analyzed file may contain more fields, such as a `Redaction` section to indicate that there is redacted data in the redacted analysis file\.

## Categories<a name="chat-categories"></a>

`PointsOfInterest` differs between post\-chat and post\-call categories:
+ Post\-call `PointsOfInterest` has milliseconds offset\. 
+ Post\-chat `PointsOfInterest` has an array of `TranscriptItems`; each item has an `id` and `CharacterOffset`\.

There is an array of `PointsOfInterest`\. Each array has an array of `TranscriptItems`: each `PointOfInterest` is for a Category match, but each match can span across multiple transcript items\.

For both calls and chats, the `PointsOfInterest` array can be empty\. This means that the category is matched for the whole contact\. For example, if you create a rule to match the category when `Hello` is not mentioned in the contact, there would be no portion of the transcript to pinpoint for this condition\.

**Note**  
Currently, category is inferred for `text/plain`, `text/markdown` chat messages only\.

## Contact summary<a name="chat-contactsummary"></a>

Contact summary is located in the `ConversationCharacteristics.ContactSummary.SummaryItemsDetected` array\. No more than one item can be in that array, emphasizing that only one set of `Issue`, `Outcome`, and `Action` item can be found\. 

Each object in the array has following fields: `IssuesDetected`, `OutcomesDetected`, `ActionItemsDetected`\.

Each of the fields has an array of `TranscriptItems` that has `Id` and `CharacterOffsets`\. They describe `TranscriptItems` and specific parts that were identified to contain that contact summary: issue, outcome, or action item\.

**Note**  
Currently, contact summary is inferred for `text/plain` chat messages only\.

## Sentiment<a name="chat-sentiment"></a>

### Overall sentiment<a name="chat-overallsentiment"></a>

The `DetailsByParticipantRole` field sentiment score for contact participants is similar to Contact Lens for speech analysis file\.

`DetailsByInteraction` field has `CUSTOMER` sentiment score for parts of chat interaction `WithAgent` and `WithoutAgent`\. If there were no customer messages in those parts of interaction, the respective field will be absent\.

**Note**  
Currently, sentiment is inferred is for `text/plain`, `text/markdown` chat messages only\.

### Sentiment shift<a name="chat-sentimentshift"></a>

The `DetailsByParticipantRole` field contains an object that describes the sentiment shift for contact participants \(that is, `AGENT`, `CUSTOMER`\): `BeginScore` and `EndScore`\. 

The `DetailsByInteraction` field has `CUSTOMER` sentiment shift for parts of the chat interaction `WithAgent` and `WithoutAgent`\. If there were no customer messages in those parts of the interaction, the respective field will be absent\.

Sentiment shift provides information about how the participant's sentiment changed throughout the chat interaction\.

## Response time<a name="chat-responsetime"></a>

`AgentGreetingTimeMillis` measures the time between when the `AGENT` joined the chat and the moment when they ended their first message to customer\.

`DetailsByParticipantRole` has following characteristics for each of participant:
+ `Average`: What is average response time for a participant\.
+ `Maximum`: What is the longest response time for a participant\. If there are multiple transcript items with the same maximum response time, which ones are they\.

To calculate the `Average` and `Maximum` response times for a given participant, they need to respond to a message from another participant \(`AGENT` needs to responds to the `CUSTOMER`, or vice versa\)\. 

For example, if there was only one message from `CUSTOMER` and then only one message from `AGENT` before the chat ended, Contact Lens will calculate a response time for the `AGENT`, but not for the `CUSTOMER`\. 

**Note**  
Currently, response time is inferred is for ` text/plain`, `text/markdown` chat messages only\.

## Redaction<a name="chat-redaction"></a>

Note the following about the original analysis file for chats:
+ Transcript item includes a `Redaction` section only if it there is data to be redacted\. The section contains character offsets for the data that is redacted in the redacted analysis file\. 
+ If two or more pieces of a message are redacted, the first offset applies to the first redacted piece, the second offset applies to the second redacted piece, and so on\.

`DisplayNames` for `AGENT` and `CUSTOMER` are redacted because they contain PII\. This applies to `AttachmentName`, too\.

`CharacterOffsets` take into consideration redaction changes of the `Content` length in the redacted analysis file\. `CharacterOffsets` describe redacted content, not original content\.

## Example original chat file<a name="chat-exampleoriginalfile"></a>

```
{
    "AccountId": "123456789012",
    "Categories": {
        "MatchedCategories": [
            "agent-intro"
        ],
        "MatchedDetails": {
            "agent-intro": {
                "PointsOfInterest": [
                    {
                        "TranscriptItems": [
                            {
                                "CharacterOffsets": {
                                    "BeginOffsetChar": 0,
                                    "EndOffsetChar": 73
                                },
                                "Id": "e4949dd1-aaa1-4fbd-84e7-65c95b2d3d9a"
                            }
                        ]
                    }
                ]
            }
        }
    },
    "Channel": "CHAT",
    "ChatTranscriptVersion": "2019-08-26",
    "ContentMetadata": {
        "Output": "Raw"
    },
    "ConversationCharacteristics": {
        "ContactSummary": {
            "SummaryItemsDetected": [
                {
                    "ActionItemsDetected": [],
                    "IssuesDetected": [
                        {
                            "TranscriptItems": [
                                {
                                    "CharacterOffsets": {
                                        "BeginOffsetChar": 72,
                                        "EndOffsetChar": 244
                                    },
                                    "Id": "2b8ba020-53ee-4053-b5b7-35364ac1c7df"
                                }
                            ]
                        }
                    ],
                    "OutcomesDetected": [
                        {
                            "TranscriptItems": [
                                {
                                    "CharacterOffsets": {
                                        "BeginOffsetChar": 0,
                                        "EndOffsetChar": 150
                                    },
                                    "Id": "72cc8c8d-2199-422a-b363-01d6d3fdc851"
                                }
                            ]
                        }
                    ]
                }
            ]
        },
        "ResponseTime": {
            "AgentGreetingTimeMillis": 2511,
            "DetailsByParticipantRole": {
                "AGENT": {
                    "Average": {
                        "ValueMillis": 5575
                    },
                    "Maximum": {
                        "TranscriptItems": [
                            {
                                "Id": "21acf0fc-7259-4a08-b4cd-688eb56587d3"
                            }
                        ],
                        "ValueMillis": 7309
                    }
                },
                "CUSTOMER": {
                    "Average": {
                        "ValueMillis": 5875
                    },
                    "Maximum": {
                        "TranscriptItems": [
                            {
                                "Id": "c71ad383-f876-4bb3-b254-7837b6a3d395"
                            }
                        ],
                        "ValueMillis": 11366
                    }
                }
            }
        },
        "Sentiment": {
            "DetailsByTranscriptItemGroup": [
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "e4949dd1-aaa1-4fbd-84e7-65c95b2d3d9a"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3673d926-6e75-4620-a6f0-7ea571790a15"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "46d37141-32d8-4f2e-a664-bcd3f34a68b3"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3c4a2a1e-6790-46a6-8ad4-4a0980b04795"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "f9cd41b6-3f68-4e83-a47d-664395f324c0"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "21acf0fc-7259-4a08-b4cd-688eb56587d3"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "2b8ba020-53ee-4053-b5b7-35364ac1c7df"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "28d0a1ce-64d1-4625-bbef-4cfeb97b6742"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "ef9b8622-32d5-4cfd-9ccc-a242502267bc"
                        },
                        {
                            "Id": "03a9de67-f9e1-4884-a1a3-ecea78a4ce9e"
                        },
                        {
                            "Id": "cfee5ece-a671-4a11-9ec2-89aba4b7d688"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "72cc8c8d-2199-422a-b363-01d6d3fdc851"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "61bb2591-fe87-44e4-bba0-a3619c4cef1f"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "1761f27e-0989-4b6d-a046-fc03d2c6bc9c"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 3.3333333333333335,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "8cdff161-dc25-44e6-986f-fc0e08ee0a7d"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -1.6666666666666667,
                    "Sentiment": "NEGATIVE",
                    "TranscriptItems": [
                        {
                            "Id": "bcc51949-3a79-4398-be1b-a27345a8a8ad"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -3.75,
                    "Sentiment": "NEGATIVE",
                    "TranscriptItems": [
                        {
                            "Id": "7d5c07d7-3d26-4b34-ae91-39aeaeef685c"
                        },
                        {
                            "Id": "e0efbd17-9139-439b-8c80-ebf2b9b703b9"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -3.75,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "8fbb8dd4-9fd4-4991-83dc-5f06eeead9aa"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -2.5,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3b856fd9-0eeb-4fb2-93ed-95ec4aeae3a6"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "ecb8c498-96d7-448b-8360-366eeddb4090"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "d334058f-e3de-4cf1-a361-32e4e61f1839"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3ec6adb5-3f11-409c-af39-40cf7ba6f078"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "c71ad383-f876-4bb3-b254-7837b6a3d395"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "4b292b64-4a33-45ff-89df-d5a175d16d70"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "2da5a3c2-9d1b-458c-ae53-759a4e63198d"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "e23a2331-f3fc-4d3c-8a51-1541451186c9"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 3.75,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "5a27cc39-9b73-4ebe-9275-5e6723788a1b"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 3.75,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "540368c7-ec19-4fc0-8c86-0a5ee62d31a0"
                        }
                    ]
                }
            ],
            "OverallSentiment": {
                "DetailsByInteraction": {
                    "DetailsByParticipantRole": {
                        "CUSTOMER": {
                            "WithAgent": 0
                        }
                    }
                },
                "DetailsByParticipantRole": {
                    "AGENT": 1.1538461538461537,
                    "CUSTOMER": 0
                }
            },
            "SentimentShift": {
                "DetailsByInteraction": {
                    "DetailsByParticipantRole": {
                        "CUSTOMER": {
                            "WithAgent": {
                                "BeginScore": -3,
                                "EndScore": 3.75
                            }
                        }
                    }
                },
                "DetailsByParticipantRole": {
                    "AGENT": {
                        "BeginScore": 0,
                        "EndScore": 2.5
                    },
                    "CUSTOMER": {
                        "BeginScore": -3.75,
                        "EndScore": 3.75
                    },
                    "SYSTEM": {
                        "BeginScore": 2.5,
                        "EndScore": 0
                    }
                }
            }
        }
    },
    "CustomerMetadata": {
        "ContactId": "b49644f6-672f-445c-b209-f76b36482830",
        "InputS3Uri": "path to the json file in s3",
        "InstanceId": "f23fc323-3d6d-48aa-95dc-EXAMPLE012"
    },
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "Participants": [
        {
            "DisplayName": "John",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER"
        },
        {
            "DisplayName": "SYSTEM_MESSAGE",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM"
        },
        {
            "DisplayName": "Jane",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT"
        }
    ],
    "Transcript": [
        {
            "AbsoluteTime": "2022-10-27T03:31:50.735Z",
            "ContentType": "application/vnd.amazonaws.connect.event.participant.joined",
            "DisplayName": "John",
            "Id": "740c494d-9df7-4400-91c0-3e4df33922c8",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "EVENT"
        },
        {
            "AbsoluteTime": "2022-10-27T03:31:53.390Z",
            "Content": "Hello, thanks for contacting us. This is an example of what the Amazon Connect virtual contact center can enable you to do.",
            "ContentType": "text/plain",
            "DisplayName": "SYSTEM_MESSAGE",
            "Id": "78aa8229-714a-4c87-916b-ce7d8d567ab2",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:31:55.131Z",
            "Content": "The time in queue is less than 5 minutes.",
            "ContentType": "text/plain",
            "DisplayName": "SYSTEM_MESSAGE",
            "Id": "1276382b-facb-49c5-8d34-62e3b0f50002",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:31:56.618Z",
            "Content": "You are now being placed in queue to chat with an agent.",
            "ContentType": "text/plain",
            "DisplayName": "SYSTEM_MESSAGE",
            "Id": "88c2363e-8206-4781-a353-c15e1ccacc12",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:00.951Z",
            "ContentType": "application/vnd.amazonaws.connect.event.participant.joined",
            "DisplayName": "Jane",
            "Id": "c05cca74-d50b-4aa5-b46c-fdb5ae8c814c",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "EVENT"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:03.462Z",
            "Content": "Hello, thanks for reaching Example Corp. This is Jane. How may I help you?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "e4949dd1-aaa1-4fbd-84e7-65c95b2d3d9a",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 46,
                        "EndOffsetChar": 53
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:08.102Z",
            "Content": "I'd like to see if I can get a refund or an exchange, because I ordered one of your grow-it-yourself indoor herb garden kits and nothing sprouted after a couple weeks so I think something is wrong with the seeds and this product may be defective.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "bcc51949-3a79-4398-be1b-a27345a8a8ad",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:14.137Z",
            "Content": "My wife is blind and sensitive to the sun so I was going to surprise her for her birthday with all the herbs that she loves so you guys actually really let me down.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "7d5c07d7-3d26-4b34-ae91-39aeaeef685c",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:18.781Z",
            "Content": "I should be taking my business elsewhere. I don't see why I should be giving money to a company that isn't even going to sell a product that works.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "e0efbd17-9139-439b-8c80-ebf2b9b703b9",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:24.123Z",
            "Content": "Ok. Can I get your first and last name please?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "3673d926-6e75-4620-a6f0-7ea571790a15",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:29.879Z",
            "Content": "Yeah. My first name is John and last name is Doe.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "8fbb8dd4-9fd4-4991-83dc-5f06eeead9aa",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 21,
                        "EndOffsetChar": 26
                    },
                    {
                        "BeginOffsetChar": 44,
                        "EndOffsetChar": 49
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:34.670Z",
            "Content": "Could you please provide me with the order ID number?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "46d37141-32d8-4f2e-a664-bcd3f34a68b3",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:39.726Z",
            "Content": "Yes, just . Looking ...",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "3b856fd9-0eeb-4fb2-93ed-95ec4aeae3a6",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:44.887Z",
            "Content": "Not a problem, take your time.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "3c4a2a1e-6790-46a6-8ad4-4a0980b04795",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:52.978Z",
            "Content": "Okay, that should be #5376897. You know, if the product was fine I wouldn't have to scrounge through emails.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "ecb8c498-96d7-448b-8360-366eeddb4090",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:59.441Z",
            "Content": "alright, perfect. And could you also just confirm the shipping address for me?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "f9cd41b6-3f68-4e83-a47d-664395f324c0",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 77,
                        "EndOffsetChar": 78
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:05.455Z",
            "Content": "123 Any Street, Any Town, and the zip code is 98109.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "d334058f-e3de-4cf1-a361-32e4e61f1839",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 0,
                        "EndOffsetChar": 27
                    },
                    {
                        "BeginOffsetChar": 49,
                        "EndOffsetChar": 54
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:12.764Z",
            "Content": "Thank you very much. Just waiting on my system here. .. I'll also need the last four digits of your debit card.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "21acf0fc-7259-4a08-b4cd-688eb56587d3",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:17.412Z",
            "Content": "Ok. Last four for my debit care are 9008",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "3ec6adb5-3f11-409c-af39-40cf7ba6f078",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 27,
                        "EndOffsetChar": 31
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:22.486Z",
            "Content": "It's just too bad. I thought this was going to be the best gift idea. How can you guys be sending out defective seeds? Isn't that your whole business?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "2b8ba020-53ee-4053-b5b7-35364ac1c7df",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },        
        {
            "AbsoluteTime": "2022-10-27T03:33:38.961Z",
            "Content": "I apologize for the experience you had Mr. Doe, its very uncommon that our customer will have this issue. We will look into this and get this sorted out for you right away.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "28d0a1ce-64d1-4625-bbef-4cfeb97b6742",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 41,
                        "EndOffsetChar": 46
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:44.192Z",
            "Content": "Well, my wife's birthday already passed, so. There's not too much you can do. But I would still like to grow the herbs for her, if possible.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "4b292b64-4a33-45ff-89df-d5a175d16d70",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:51.310Z",
            "Content": "Totally understandable. Let me see what we can do for you. Please give me couple of minutes as I check the system.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "ef9b8622-32d5-4cfd-9ccc-a242502267bc",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:56.287Z",
            "Content": "Thank you sir one moment please.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "03a9de67-f9e1-4884-a1a3-ecea78a4ce9e",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:01.224Z",
            "Content": "Alright are you still there Mr Doe?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "cfee5ece-a671-4a11-9ec2-89aba4b7d688",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 30,
                        "EndOffsetChar": 35
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:07.093Z",
            "Content": "Yeah.",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "2da5a3c2-9d1b-458c-ae53-759a4e63198d",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:12.562Z",
            "Content": "We are not only refunding the cost of the grow-it-yourself indoor herb kit but we will also be sending you a replacement. Would you be okay with this?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "72cc8c8d-2199-422a-b363-01d6d3fdc851",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:17.029Z",
            "Content": "Yeah! That would be great. I just want my wife to be able to have these herbs in her room. And I'm always happy to get my money back!",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "e23a2331-f3fc-4d3c-8a51-1541451186c9",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:22.269Z",
            "Content": "Awesome! We really want to keep our customers happy and satisfied, and again I want to apologize for your less than satisfactory experience with the last product you ordered from us.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "61bb2591-fe87-44e4-bba0-a3619c4cef1f",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:26.353Z",
            "Content": "Okay! No problem. Sounds great. Thank you for all your help!",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "5a27cc39-9b73-4ebe-9275-5e6723788a1b",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:31.431Z",
            "Content": "Is there anything else I can help you out with John?",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "1761f27e-0989-4b6d-a046-fc03d2c6bc9c",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 48,
                        "EndOffsetChar": 53
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:36.704Z",
            "Content": "Nope!",
            "ContentType": "text/markdown",
            "DisplayName": "John",
            "Id": "540368c7-ec19-4fc0-8c86-0a5ee62d31a0",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:41.448Z",
            "Content": "Ok great! Have a great day.",
            "ContentType": "text/markdown",
            "DisplayName": "Jane",
            "Id": "8cdff161-dc25-44e6-986f-fc0e08ee0a7d",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:42.799Z",
            "ContentType": "application/vnd.amazonaws.connect.event.participant.left",
            "DisplayName": "John",
            "Id": "d1ba54ba-61d4-4a48-9a9a-6cd17d70b8fb",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "EVENT"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:43.192Z",
            "ContentType": "application/vnd.amazonaws.connect.event.chat.ended",
            "Id": "2d9a0e4f-faec-485f-97af-2767dde1f30a",
            "Type": "EVENT"
        }
    ],
    "Version": "CHAT-2022-11-30"
}
```

## Example redacted chat file<a name="chat-exampleredactedfile"></a>

```
{
    "AccountId": "123456789012",
    "Categories": {
        "MatchedCategories": [
            "agent-intro"
        ],
        "MatchedDetails": {
            "agent-intro": {
                "PointsOfInterest": [
                    {
                        "TranscriptItems": [
                            {
                                "CharacterOffsets": {
                                    "BeginOffsetChar": 0,
                                    "EndOffsetChar": 71
                                },
                                "Id": "e4949dd1-aaa1-4fbd-84e7-65c95b2d3d9a"
                            }
                        ]
                    }
                ]
            }
        }
    },
    "Channel": "CHAT",
    "ChatTranscriptVersion": "2019-08-26",
    "ContentMetadata": {
        "Output": "Redacted",
        "RedactionTypes": [
            "PII"
        ],
        "RedactionTypesMetadata": {
            "PII": {
                "RedactionMaskMode": "PII"
            }
        }
    },
    "ConversationCharacteristics": {
        "ContactSummary": {
            "SummaryItemsDetected": [
                {
                    "ActionItemsDetected": [],
                    "IssuesDetected": [
                        {
                            "TranscriptItems": [
                                {
                                    "CharacterOffsets": {
                                        "BeginOffsetChar": 72,
                                        "EndOffsetChar": 244
                                    },
                                    "Id": "2b8ba020-53ee-4053-b5b7-35364ac1c7df"
                                }
                            ]
                        }
                    ],
                    "OutcomesDetected": [
                        {
                            "TranscriptItems": [
                                {
                                    "CharacterOffsets": {
                                        "BeginOffsetChar": 0,
                                        "EndOffsetChar": 150
                                    },
                                    "Id": "72cc8c8d-2199-422a-b363-01d6d3fdc851"
                                }
                            ]
                        }
                    ]
                }
            ]
        },
        "ResponseTime": {
            "AgentGreetingTimeMillis": 2511,
            "DetailsByParticipantRole": {
                "AGENT": {
                    "Average": {
                        "ValueMillis": 5575
                    },
                    "Maximum": {
                        "TranscriptItems": [
                            {
                                "Id": "21acf0fc-7259-4a08-b4cd-688eb56587d3"
                            }
                        ],
                        "ValueMillis": 7309
                    }
                },
                "CUSTOMER": {
                    "Average": {
                        "ValueMillis": 5875
                    },
                    "Maximum": {
                        "TranscriptItems": [
                            {
                                "Id": "c71ad383-f876-4bb3-b254-7837b6a3d395"
                            }
                        ],
                        "ValueMillis": 11366
                    }
                }
            }
        },
        "Sentiment": {
            "DetailsByTranscriptItemGroup": [
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "e4949dd1-aaa1-4fbd-84e7-65c95b2d3d9a"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3673d926-6e75-4620-a6f0-7ea571790a15"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "46d37141-32d8-4f2e-a664-bcd3f34a68b3"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3c4a2a1e-6790-46a6-8ad4-4a0980b04795"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "f9cd41b6-3f68-4e83-a47d-664395f324c0"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "21acf0fc-7259-4a08-b4cd-688eb56587d3"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "2b8ba020-53ee-4053-b5b7-35364ac1c7df"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "28d0a1ce-64d1-4625-bbef-4cfeb97b6742"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "ef9b8622-32d5-4cfd-9ccc-a242502267bc"
                        },
                        {
                            "Id": "03a9de67-f9e1-4884-a1a3-ecea78a4ce9e"
                        },
                        {
                            "Id": "cfee5ece-a671-4a11-9ec2-89aba4b7d688"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "72cc8c8d-2199-422a-b363-01d6d3fdc851"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "61bb2591-fe87-44e4-bba0-a3619c4cef1f"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "1761f27e-0989-4b6d-a046-fc03d2c6bc9c"
                        }
                    ]
                },
                {
                    "ParticipantRole": "AGENT",
                    "ProgressiveScore": 3.3333333333333335,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "8cdff161-dc25-44e6-986f-fc0e08ee0a7d"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -1.6666666666666667,
                    "Sentiment": "NEGATIVE",
                    "TranscriptItems": [
                        {
                            "Id": "bcc51949-3a79-4398-be1b-a27345a8a8ad"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -3.75,
                    "Sentiment": "NEGATIVE",
                    "TranscriptItems": [
                        {
                            "Id": "7d5c07d7-3d26-4b34-ae91-39aeaeef685c"
                        },
                        {
                            "Id": "e0efbd17-9139-439b-8c80-ebf2b9b703b9"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -3.75,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "8fbb8dd4-9fd4-4991-83dc-5f06eeead9aa"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": -2.5,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3b856fd9-0eeb-4fb2-93ed-95ec4aeae3a6"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "ecb8c498-96d7-448b-8360-366eeddb4090"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "d334058f-e3de-4cf1-a361-32e4e61f1839"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "3ec6adb5-3f11-409c-af39-40cf7ba6f078"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "c71ad383-f876-4bb3-b254-7837b6a3d395"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "4b292b64-4a33-45ff-89df-d5a175d16d70"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 0,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "2da5a3c2-9d1b-458c-ae53-759a4e63198d"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 1.6666666666666667,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "e23a2331-f3fc-4d3c-8a51-1541451186c9"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 3.75,
                    "Sentiment": "POSITIVE",
                    "TranscriptItems": [
                        {
                            "Id": "5a27cc39-9b73-4ebe-9275-5e6723788a1b"
                        }
                    ]
                },
                {
                    "ParticipantRole": "CUSTOMER",
                    "ProgressiveScore": 3.75,
                    "Sentiment": "NEUTRAL",
                    "TranscriptItems": [
                        {
                            "Id": "540368c7-ec19-4fc0-8c86-0a5ee62d31a0"
                        }
                    ]
                }
            ],
            "OverallSentiment": {
                "DetailsByInteraction": {
                    "DetailsByParticipantRole": {
                        "CUSTOMER": {
                            "WithAgent": 0
                        }
                    }
                },
                "DetailsByParticipantRole": {
                    "AGENT": 1.1538461538461537,
                    "CUSTOMER": 0
                }
            },
            "SentimentShift": {
                "DetailsByInteraction": {
                    "DetailsByParticipantRole": {
                        "CUSTOMER": {
                            "WithAgent": {
                                "BeginScore": -3,
                                "EndScore": 3.75
                            }
                        }
                    }
                },
                "DetailsByParticipantRole": {
                    "AGENT": {
                        "BeginScore": 0,
                        "EndScore": 2.5
                    },
                    "CUSTOMER": {
                        "BeginScore": -3.75,
                        "EndScore": 3.75
                    }
                }
            }
        }
    },
    "CustomerMetadata": {
        "ContactId": "b49644f6-672f-445c-b209-f76b36482830",
        "InputS3Uri": "path to the json file in s3",
        "InstanceId": "f23fc323-3d6d-48aa-EXAMPLE012"
    },
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "Participants": [
        {
            "DisplayName": "[PII]",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8"
        },
        {
            "DisplayName": "SYSTEM_MESSAGE",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02"
        },
        {
            "DisplayName": "[PII]",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7"
        }
    ],
    "Transcript": [
        {
            "AbsoluteTime": "2022-10-27T03:31:50.735Z",
            "ContentType": "application/vnd.amazonaws.connect.event.participant.joined",
            "DisplayName": "[PII]",
            "Id": "740c494d-9df7-4400-91c0-3e4df33922c8",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "EVENT"
        },
        {
            "AbsoluteTime": "2022-10-27T03:31:53.390Z",
            "Content": "Hello, thanks for contacting us. This is an example of what the Amazon Connect virtual contact center can enable you to do.",
            "ContentType": "text/plain",
            "DisplayName": "SYSTEM_MESSAGE",
            "Id": "78aa8229-714a-4c87-916b-ce7d8d567ab2",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:31:55.131Z",
            "Content": "The time in queue is less than 5 minutes.",
            "ContentType": "text/plain",
            "DisplayName": "SYSTEM_MESSAGE",
            "Id": "1276382b-facb-49c5-8d34-62e3b0f50002",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:31:56.618Z",
            "Content": "You are now being placed in queue to chat with an agent.",
            "ContentType": "text/plain",
            "DisplayName": "SYSTEM_MESSAGE",
            "Id": "88c2363e-8206-4781-a353-c15e1ccacc12",
            "ParticipantId": "2b2288b4-ff6e-4996-8d8e-260fd5a8ac02",
            "ParticipantRole": "SYSTEM",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:00.951Z",
            "ContentType": "application/vnd.amazonaws.connect.event.participant.joined",
            "DisplayName": "[PII]",
            "Id": "c05cca74-d50b-4aa5-b46c-fdb5ae8c814c",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "EVENT"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:03.462Z",
            "Content": "Hello, thanks for reaching Example Corp. This is [PII]. How may I help you?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "e4949dd1-aaa1-4fbd-84e7-65c95b2d3d9a",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 46,
                        "EndOffsetChar": 51
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:08.102Z",
            "Content": "I'd like to see if I can get a refund or an exchange, because I ordered one of your grow-it-yourself indoor herb garden kits and nothing sprouted after a couple weeks so I think something is wrong with the seeds and this product may be defective.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "bcc51949-3a79-4398-be1b-a27345a8a8ad",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:14.137Z",
            "Content": "My wife is blind and sensitive to the sun so I was going to surprise her for her birthday with all the herbs that she loves so you guys actually really let me down.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "7d5c07d7-3d26-4b34-ae91-39aeaeef685c",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:18.781Z",
            "Content": "I should be taking my business elsewhere. I don't see why I should be giving money to a company that isn't even going to sell a product that works.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "e0efbd17-9139-439b-8c80-ebf2b9b703b9",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:24.123Z",
            "Content": "Ok. Can I get your first and last name please?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "3673d926-6e75-4620-a6f0-7ea571790a15",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:29.879Z",
            "Content": "Yeah. My first name is [PII] and last name [PII].",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "8fbb8dd4-9fd4-4991-83dc-5f06eeead9aa",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 21,
                        "EndOffsetChar": 26
                    },
                    {
                        "BeginOffsetChar": 44,
                        "EndOffsetChar": 49
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:34.670Z",
            "Content": "Could you please provide me with the order ID number?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "46d37141-32d8-4f2e-a664-bcd3f34a68b3",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:39.726Z",
            "Content": "Yes, just . Looking ...",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "3b856fd9-0eeb-4fb2-93ed-95ec4aeae3a6",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:44.887Z",
            "Content": "Not a problem, take your time.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "3c4a2a1e-6790-46a6-8ad4-4a0980b04795",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:52.978Z",
            "Content": "Okay, that should be #5376897. You know, if the product was fine I wouldn't have to scrounge through emails.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "ecb8c498-96d7-448b-8360-366eeddb4090",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:32:59.441Z",
            "Content": "alright, perfect. And could you also just confirm the shipping address for me, [PII]",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "f9cd41b6-3f68-4e83-a47d-664395f324c0",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 77,
                        "EndOffsetChar": 82
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:05.455Z",
            "Content": "[PII], and the zip code [PII].",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "d334058f-e3de-4cf1-a361-32e4e61f1839",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 0,
                        "EndOffsetChar": 5
                    },
                    {
                        "BeginOffsetChar": 27,
                        "EndOffsetChar": 32
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:12.764Z",
            "Content": "Thank you very much. Just waiting on my system here. .. I'll also need the last four digits of your debit card.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "21acf0fc-7259-4a08-b4cd-688eb56587d3",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:17.412Z",
            "Content": "Ok. Last four for my debit card [PII]",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "3ec6adb5-3f11-409c-af39-40cf7ba6f078",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 27,
                        "EndOffsetChar": 32
                    }
                ]
            },
            "Type": "MESSAGE"
        },        
        {
            "AbsoluteTime": "2022-10-27T03:33:33.852Z",
            "Content": "It's just too bad. I thought this was going to be the best gift idea. How can you guys be sending out defective seeds? Isn't that your whole business?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "c71ad383-f876-4bb3-b254-7837b6a3d395",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:38.961Z",
            "Content": "I apologize for the experience you had Mr [PII], its very uncommon that our customer will have this issue. We will look into this and get this sorted out for you right away.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "28d0a1ce-64d1-4625-bbef-4cfeb97b6742",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 41,
                        "EndOffsetChar": 46
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:44.192Z",
            "Content": "Well, my wife's birthday already passed, so. There's not too much you can do. But I would still like to grow the herbs for her, if possible.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "4b292b64-4a33-45ff-89df-d5a175d16d70",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:51.310Z",
            "Content": "Totally understandable. Let me see what we can do for you. Please give me couple of minutes as I check the system.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "ef9b8622-32d5-4cfd-9ccc-a242502267bc",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:33:56.287Z",
            "Content": "Thank you sir one moment please.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "03a9de67-f9e1-4884-a1a3-ecea78a4ce9e",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:01.224Z",
            "Content": "Alright are you still there Mr [PII]?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "cfee5ece-a671-4a11-9ec2-89aba4b7d688",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 30,
                        "EndOffsetChar": 35
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:07.093Z",
            "Content": "Yeah.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "2da5a3c2-9d1b-458c-ae53-759a4e63198d",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:12.562Z",
            "Content": "We are not only refunding the cost of the grow-it-yourself indoor herb kit but we will also be sending you a replacement. Would you be okay with this?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "72cc8c8d-2199-422a-b363-01d6d3fdc851",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:17.029Z",
            "Content": "Yeah! That would be great. I just want my wife to be able to have these herbs in her room. And I'm always happy to get my money back!",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "e23a2331-f3fc-4d3c-8a51-1541451186c9",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:22.269Z",
            "Content": "Awesome! We really want to keep our customers happy and satisfied, and again I want to apologize for your less than satisfactory experience with the last product you ordered from us.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "61bb2591-fe87-44e4-bba0-a3619c4cef1f",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:26.353Z",
            "Content": "Okay! No problem. Sounds great. Thank you for all your help!",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "5a27cc39-9b73-4ebe-9275-5e6723788a1b",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:31.431Z",
            "Content": "Is there anything else I can help you out with Mr [PII]?",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "1761f27e-0989-4b6d-a046-fc03d2c6bc9c",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Redaction": {
                "CharacterOffsets": [
                    {
                        "BeginOffsetChar": 48,
                        "EndOffsetChar": 53
                    }
                ]
            },
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:36.704Z",
            "Content": "Nope!",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "540368c7-ec19-4fc0-8c86-0a5ee62d31a0",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:41.448Z",
            "Content": "Ok great! Have a great day.",
            "ContentType": "text/plain",
            "DisplayName": "[PII]",
            "Id": "8cdff161-dc25-44e6-986f-fc0e08ee0a7d",
            "ParticipantId": "f36a545d-67b2-4fd4-89fb-896136b609a7",
            "ParticipantRole": "AGENT",
            "Type": "MESSAGE"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:42.799Z",
            "ContentType": "application/vnd.amazonaws.connect.event.participant.left",
            "DisplayName": "[PII]",
            "Id": "d1ba54ba-61d4-4a48-9a9a-6cd17d70b8fb",
            "ParticipantId": "e9b36a6d-12aa-4c21-9745-1881648ecfc8",
            "ParticipantRole": "CUSTOMER",
            "Type": "EVENT"
        },
        {
            "AbsoluteTime": "2022-10-27T03:34:43.192Z",
            "ContentType": "application/vnd.amazonaws.connect.event.chat.ended",
            "Id": "2d9a0e4f-faec-485f-97af-2767dde1f30a",
            "Type": "EVENT"
        }
    ],
    "Version": "CHAT-2022-11-30"
}
```