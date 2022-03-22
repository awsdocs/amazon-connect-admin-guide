# Example Contact Lens output files<a name="contact-lens-example-output-files"></a>

## Example output locations<a name="example-contact-lens-output-locations"></a>

Following are examples of what Contact Lens output files look like when they are stored in the Amazon S3 bucket for your instance\. 
+ Original analyzed transcript file \(JSON\)
  + /connect\-instance\- bucket/**Analysis/Voice**/2020/02/04/*contact's\_ID*\_**analysis**\_2020\-02\-04T21:14:16Z\.json
+ Redacted analyzed transcript file in \(JSON\)
  + /connect\-instance\- bucket/**Analysis/Voice/Redacted**/2020/02/04/*contact's\_ID*\_**analysis\_redacted**\_2020\-02\-04T21:14:16Z\.json
+ Redacted audio file
  + /connect\-instance\- bucket/**Analysis/Voice/Redacted**/2020/02/04/*contact's\_ID*\_**call\_recording\_redacted**\_2020\-02\-04T21:14:16Z\.**wav**

## Example original, analyzed file<a name="example-original-output-file"></a>

This section shows an example schema for a conversation that Contact Lens has analyzed\. The example shows loudness, issue detection/call drivers, and what information is going to be redacted\.

Note the following about the analyzed file:
+ It doesn't indicate what sensitive data was redacted\. All data are referred to as PII \(personally identifiable information\)\.
+ Each turn includes a `Redacted` section only if it includes PII\.
+ If a `Redacted` section exists, it includes the offset in milliseconds\. In a \.wav file, the redacted portion will be silence\. If desired, you can use the offset to replace the silence with something else, such as a beep\. 
+ If two or more PII redactions exist in a turn, the first offset applies to the first PII, the second offset applies to the second PII, and so on\.

```
{
    "Version": "1.1.0",
    "AccountId": "your AWS account ID",
    "Channel": "VOICE",
    "ContentMetadata": {
        "Output": "Raw" 
    },
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "Participants": [
        {
            "ParticipantId": "the customer's ID",
            "ParticipantRole": "CUSTOMER"
        },
        {
            "ParticipantId": "the agent's ID",
            "ParticipantRole": "AGENT"
        }
    ],
    "Categories": {
        "MatchedCategories": [],
        "MatchedDetails": {}
    },
    "ConversationCharacteristics": {
        "TotalConversationDurationMillis": 32110,
        "Sentiment": {
            "OverallSentiment": {
                "AGENT": 0,
                "CUSTOMER": 3.1
            },
            "SentimentByPeriod": {
                "QUARTER": {
                    "AGENT": [
                        {
                            "BeginOffsetMillis": 0,
                            "EndOffsetMillis": 7427,
                            "Score": 0
                        },
                        {
                            "BeginOffsetMillis": 7427,
                            "EndOffsetMillis": 14855,
                            "Score": -5
                        },
                        {
                            "BeginOffsetMillis": 14855,
                            "EndOffsetMillis": 22282,
                            "Score": 0
                        },
                        {
                            "BeginOffsetMillis": 22282,
                            "EndOffsetMillis": 29710,
                            "Score": 5
                        }
                    ],
                    "CUSTOMER": [
                        {
                            "BeginOffsetMillis": 0,
                            "EndOffsetMillis": 8027,
                            "Score": -2.5
                        },
                        {
                            "BeginOffsetMillis": 8027,
                            "EndOffsetMillis": 16055,
                            "Score": 5
                        },
                        {
                            "BeginOffsetMillis": 16055,
                            "EndOffsetMillis": 24082,
                            "Score": 5
                        },
                        {
                            "BeginOffsetMillis": 24082,
                            "EndOffsetMillis": 32110,
                            "Score": 5
                        }
                    ]
                }
            }
        },
        "Interruptions": {
            "InterruptionsByInterrupter": {},
            "TotalCount": 0,
            "TotalTimeMillis": 0
        },
        "NonTalkTime": {
            "TotalTimeMillis": 0,
            "Instances": []
        },
        "TalkSpeed": {
            "DetailsByParticipant": {
                "AGENT": {
                    "AverageWordsPerMinute": 239
                },
                "CUSTOMER": {
                    "AverageWordsPerMinute": 163
                }
            }
        },
        "TalkTime": {
            "TotalTimeMillis": 28698,
            "DetailsByParticipant": {
                "AGENT": {
                    "TotalTimeMillis": 15079
                },
                "CUSTOMER": {
                    "TotalTimeMillis": 13619
                }
            }
        }
    },
    "CustomModels": [], 
    "Transcript": [
        {
            "BeginOffsetMillis": 0,
            "Content": "Okay.",
            "EndOffsetMillis": 90,
            "Id": "the ID of the turn",
            "ParticipantId": "the agent's ID",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                79.27
            ]
        },
        {
            "BeginOffsetMillis": 160,
            "Content": "Just hello. My name is Peter and help.",
            "EndOffsetMillis": 4640,
            "Id": "the ID of the turn",
            "ParticipantId": "the customer's ID",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                66.56,
                40.06,
                85.27,
                82.22,
                77.66
            ],
            "Redaction": {
                "RedactedTimestamps": [
                    {
                        "BeginOffsetMillis": 3290,
                        "EndOffsetMillis": 3620
                    }
                ]
            }
        },
        {
            "BeginOffsetMillis": 4640,
            "Content": "Hello. Peter, how can I help you?",
            "EndOffsetMillis": 6610,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                70.23,
                73.05,
                71.8
            ],
            "Redaction": {
                "RedactedTimestamps": [
                    {
                        "BeginOffsetMillis": 5100,
                        "EndOffsetMillis": 5450
                    }
                ]
            }
        },
        {
            "BeginOffsetMillis": 7370,
            "Content": "I need to cancel. I want to cancel my plan subscription.",
            "EndOffsetMillis": 11190,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "NEGATIVE",
            "LoudnessScore": [
                77.18,
                79.59,
                85.23,
                81.08,
                73.99
            ],
            "IssuesDetected": [
                {
                    "CharacterOffsets": {
                        "BeginOffsetChar": 0,
                        "EndOffsetChar": 55
                    },
                    "Text": "I need to cancel. I want to cancel my plan subscription"
                }
            ]
        },
        {
            "BeginOffsetMillis": 11220,
            "Content": "That sounds very bad. I can offer a 20% discount to make you stay with us.",
            "EndOffsetMillis": 15210,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEGATIVE",
            "LoudnessScore": [
                75.92,
                75.79,
                80.31,
                80.44,
                76.31
            ]
        },
        {
            "BeginOffsetMillis": 15840,
            "Content": "That sounds interesting. Thank you accept.",
            "EndOffsetMillis": 18120,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                73.77,
                79.17,
                77.97,
                79.29
            ]
        },
        {
            "BeginOffsetMillis": 18310,
            "Content": "Alright, I made all the changes to the account and now these discounts applied.",
            "EndOffsetMillis": 21820,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                83.88,
                86.75,
                86.97,
                86.11
            ],
            "OutcomesDetected": [
                {
                    "CharacterOffsets": {
                        "BeginOffsetChar": 9,
                        "EndOffsetChar": 77
                    },
                    "Text": "I made all the changes to the account and now these discounts applied"
                }
            ]
        },
        {
            "BeginOffsetMillis": 22610,
            "Content": "Awesome. Thank you so much.",
            "EndOffsetMillis": 24140,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                79.11,
                81.7,
                78.15
            ]
        },
        {
            "BeginOffsetMillis": 24120,
            "Content": "No worries. I will send you all the details later today and call you back next week to check up on you.",
            "EndOffsetMillis": 29710,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                87.07,
                83.96,
                76.38,
                88.38,
                87.69,
                76.6
            ],
            "ActionItemsDetected": [
                {
                    "CharacterOffsets": {
                        "BeginOffsetChar": 12,
                        "EndOffsetChar": 102
                    },
                    "Text": "I will send you all the details later today and call you back next week to check up on you"
                }
            ]
        },
        {
            "BeginOffsetMillis": 30580,
            "Content": "Thank you. Sir. Have a nice evening.",
            "EndOffsetMillis": 32110,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                81.42,
                82.29,
                73.29
            ]
        }
    ]    
    }
}
```

## Example redacted file<a name="example-redacted-file"></a>

This section shows an example redacted file\. It's a twin of the original analyzed file\. The only difference is that sensitive data are redacted\. 

```
{
    "Version": "1.1.0",
    "AccountId": "your AWS account ID",
    "ContentMetadata": {
        "RedactionTypes": [
            "PII"
        ],
        "Output": "Redacted"
    },
    "Channel": "VOICE",
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "Participants": [
        {
            "ParticipantId": "CUSTOMER",
            "ParticipantRole": "CUSTOMER"
        },
        {
            "ParticipantId": "AGENT",
            "ParticipantRole": "AGENT"
        }
    ],
    "Categories": {
        "MatchedCategories": [],
        "MatchedDetails": {}
    },
    "ConversationCharacteristics": {
        "TotalConversationDurationMillis": 32110,
        "Sentiment": {
            "OverallSentiment": {
                "AGENT": 0,
                "CUSTOMER": 3.1
            },
            "SentimentByPeriod": {
                "QUARTER": {
                    "AGENT": [
                        {
                            "BeginOffsetMillis": 0,
                            "EndOffsetMillis": 7427,
                            "Score": 0
                        },
                        {
                            "BeginOffsetMillis": 7427,
                            "EndOffsetMillis": 14855,
                            "Score": -5
                        },
                        {
                            "BeginOffsetMillis": 14855,
                            "EndOffsetMillis": 22282,
                            "Score": 0
                        },
                        {
                            "BeginOffsetMillis": 22282,
                            "EndOffsetMillis": 29710,
                            "Score": 5
                        }
                    ],
                    "CUSTOMER": [
                        {
                            "BeginOffsetMillis": 0,
                            "EndOffsetMillis": 8027,
                            "Score": -2.5
                        },
                        {
                            "BeginOffsetMillis": 8027,
                            "EndOffsetMillis": 16055,
                            "Score": 5
                        },
                        {
                            "BeginOffsetMillis": 16055,
                            "EndOffsetMillis": 24082,
                            "Score": 5
                        },
                        {
                            "BeginOffsetMillis": 24082,
                            "EndOffsetMillis": 32110,
                            "Score": 5
                        }
                    ]
                }
            }
        },
        "Interruptions": {
            "InterruptionsByInterrupter": {},
            "TotalCount": 0,
            "TotalTimeMillis": 0
        },
        "NonTalkTime": {
            "TotalTimeMillis": 0,
            "Instances": []
        },
        "TalkSpeed": {
            "DetailsByParticipant": {
                "AGENT": {
                    "AverageWordsPerMinute": 239
                },
                "CUSTOMER": {
                    "AverageWordsPerMinute": 163
                }
            }
        },
        "TalkTime": {
            "TotalTimeMillis": 28698,
            "DetailsByParticipant": {
                "AGENT": {
                    "TotalTimeMillis": 15079
                },
                "CUSTOMER": {
                    "TotalTimeMillis": 13619
                }
            }
        }
    },
    "CustomModels": [],
    "Transcript": [
        {
            "BeginOffsetMillis": 0,
            "Content": "Okay.",
            "EndOffsetMillis": 90,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                79.27
            ]
        },
        {
            "BeginOffsetMillis": 160,
            "Content": "Just hello. My name is [PII] and help.",
            "EndOffsetMillis": 4640,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                66.56,
                40.06,
                85.27,
                82.22,
                77.66
            ],
            "Redaction": {
                "RedactedTimestamps": [
                    {
                        "BeginOffsetMillis": 3290,
                        "EndOffsetMillis": 3620
                    }
                ]
            }
        },
        {
            "BeginOffsetMillis": 4640,
            "Content": "Hello. [PII], how can I help you?",
            "EndOffsetMillis": 6610,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                70.23,
                73.05,
                71.8
            ],
            "Redaction": {
                "RedactedTimestamps": [
                    {
                        "BeginOffsetMillis": 5100,
                        "EndOffsetMillis": 5450
                    }
                ]
            }
        },
        {
            "BeginOffsetMillis": 7370,
            "Content": "I need to cancel. I want to cancel my plan subscription.",
            "EndOffsetMillis": 11190,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "NEGATIVE",
            "LoudnessScore": [
                77.18,
                79.59,
                85.23,
                81.08,
                73.99
            ],
            "IssuesDetected": [
                {
                    "CharacterOffsets": {
                        "BeginOffsetChar": 0,
                        "EndOffsetChar": 55
                    },
                    "Text": "I need to cancel. I want to cancel my plan subscription"
                }
            ]
        },
        {
            "BeginOffsetMillis": 11220,
            "Content": "That sounds very bad. I can offer a 20% discount to make you stay with us.",
            "EndOffsetMillis": 15210,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEGATIVE",
            "LoudnessScore": [
                75.92,
                75.79,
                80.31,
                80.44,
                76.31
            ]
        },
        {
            "BeginOffsetMillis": 15840,
            "Content": "That sounds interesting. Thank you accept.",
            "EndOffsetMillis": 18120,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                73.77,
                79.17,
                77.97,
                79.29
            ]
        },
        {
            "BeginOffsetMillis": 18310,
            "Content": "Alright, I made all the changes to the account and now these discounts applied.",
            "EndOffsetMillis": 21820,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "NEUTRAL",
            "LoudnessScore": [
                83.88,
                86.75,
                86.97,
                86.11
            ],
            "OutcomesDetected": [
                {
                    "CharacterOffsets": {
                        "BeginOffsetChar": 9,
                        "EndOffsetChar": 77
                    },
                    "Text": "I made all the changes to the account and now these discounts applied"
                }
            ]
        },
        {
            "BeginOffsetMillis": 22610,
            "Content": "Awesome. Thank you so much.",
            "EndOffsetMillis": 24140,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                79.11,
                81.7,
                78.15
            ]
        },
        {
            "BeginOffsetMillis": 24120,
            "Content": "No worries. I will send you all the details later today and call you back next week to check up on you.",
            "EndOffsetMillis": 29710,
            "Id": "the ID of the turn",
            "ParticipantId": "AGENT",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                87.07,
                83.96,
                76.38,
                88.38,
                87.69,
                76.6
            ],
            "ActionItemsDetected": [
                {
                    "CharacterOffsets": {
                        "BeginOffsetChar": 12,
                        "EndOffsetChar": 102
                    },
                    "Text": "I will send you all the details later today and call you back next week to check up on you"
                }
            ]
        },
        {
            "BeginOffsetMillis": 30580,
            "Content": "Thank you. Sir. Have a nice evening.",
            "EndOffsetMillis": 32110,
            "Id": "the ID of the turn",
            "ParticipantId": "CUSTOMER",
            "Sentiment": "POSITIVE",
            "LoudnessScore": [
                81.42,
                82.29,
                73.29
            ]
        }
    ]    
}
```