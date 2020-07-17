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

This section shows an example schema for a conversation that Contact Lens has analyzed\. The example shows loudness, issue detection, and what information is going to be redacted\.

Note the following about the analyzed file:
+ It doesn't indicate what sensitive data was redacted\. All data are referred to as PII \(personally identifiable information\)\.
+ Each turn includes a `Redacted` section only if it includes PII\.
+ If a `Redacted` section exists, it includes the offset in milliseconds\. In a \.wav file, the redacted portion will be silence\. If desired, you can use the offset to replace the silence with something else, such as a beep\. 
+ If two or more PII redactions exist in a turn, the first offset applies to the first PII, the second offset applies to the second PII, and so on\.

```
{
    "Participants" :[ 
      { 
          "ParticipantId" :"55555555-5555-5555-5555-55555555555",   //This is the agent's ARN. It's always long.
          "ParticipantRole" :"AGENT"
      },
      { 
          "ParticipantId" :"33333333",  //This is the customer's ID. It's always short. 
          "ParticipantRole" :"CUSTOMER"
      }
   ],
    "Channel" :"VOICE",
    "AccountId" :"BBBBBBBBBBB",
    "Version": "1.0.0",
    "JobStatus" :"COMPLETED",
    "LanguageCode" :"en-US",
    "CustomModels" :[  //Large contact centers may want to use custom language models. If so, contact AWS support for help. 
      { 
          "Type" :"TRANSCRIPTION_VOCABULARY",
          "Name" :"MostCommonKeywordsTranscriptionV1"
      },
      { 
          "Type" :"TEXT_ANALYSIS_ENTITIES",
          "Name" :"Top100EntitiesV2"
      }
   ],
   "ContentMetadata" : {
        "Output": “Raw”  //Raw indicates this file includes sensitive data. 
   },
    "CustomerMetadata" :{ 
       "InputS3Uri" :"s3://connect-cccccccccccccc/connect/poc-1/CallRecordings/2019/07/22/dddddddd-dddd-dddd-dddd-dddddddddddd_20190322T23:23_UTC.wav",
       "ContactId" :"11111111-1111-1111-1111-11111111111",
       "InstanceId" :"eeeeeee-eeee-eeee-eeee-eeeeeeeeeeee"
   },
    "Transcript" :[ 
      { 
          "ParticipantId" :"55555555-5555-5555-5555-55555555555",
          "Id" :"tttttttt-tttt-tttt-tttt-tttttttt",  //Each turn has an ID.
          "Content": "Hello, my name is Jane, may I have your email id?",
          "BeginOffsetMillis" :0,
          "EndOffsetMillis" :3000,
          "Sentiment" :"NEUTRAL",//The sentiment can be neutral, positive, negative, or mixed (some negative and positive, which is rare). 
          "LoudnessScore":[ //This indicates the loudness score. Because it's a three-second sentence, there are three loudness scores. 
            40.5,              //The Amazon Connect console shows one bar for each of these values.
            55.0,
            59.3
         ],                    //If a turn doesn't include sensitive data, there is no Redaction section.
      },
      { 
          "ParticipantId" :"33333333",
          "Id" :"sssssssss-ssss-ssss-ssss-sssssssss",
          "Content": "My email id is jane@examplecorp.com.",  //If you delete this file, you won't see the email ID.
          "BeginOffsetMillis" :3000,
          "EndOffsetMillis" :3945,
          "Sentiment" :"NEGATIVE",
          "LoudnessScore":[
            40.5,
         ],
         "Redaction"  :{    //This indicates where content is going to be redacted. 
                              //From 900ms to 944ms the customer mentioned her email and it's going to be redacted.
               "RedactedTimestamps"  :[    
                  {    
                     "BeginOffsetMillis"  :  900, 
                     "EndOffsetMillis"  :  944, 
                  } 
               ] 
      },
    {
        "ParticipantId": "33333333",
        "Id": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaaa",
        "Content": "I'm having trouble submitting the application, number AAAAAAAA on the portal.
                    I tried but couldn't connect to my POC on the portal.
                    So, I'm calling on this toll free number"
        "BeginOffsetMillis": 500,
        "EndOffsetMillis": 1945,
        "Sentiment": "NEGATIVE",
       "LoudnessScore":[
            40.5,
         ],
        "Redaction": {
                "RedactedTimestamps": [{
                        "BeginOffsetMillis": 1610,
                        "EndOffsetMillis": 1700  
                }]
        }
        "IssuesDetected": [{   //This indicates the characters that are detected as issues.
           "CharacterOffsets": {
                        "BeginOffsetChar": 0,
                        "EndOffsetChar": 81
                    },
          "Text": "I'm having trouble submitting the application, number AAAAAAAA on the portal."  //This indicates what text is an issue. On the Contact Trace Record page on the
         },                                                                                          //Amazon Connect console, this text is underlined, indicating it's an issue.
               {
            "CharacterOffsets": {
                    "BeginOffsetChar": 136,
                    "EndOffsetChar": 177
              },
           "Text": "So, I'm calling on this toll free number"   
            }
        ]         
    },
  ],
    "Categories" :{ 
       "MatchedCategories" :[ //These are the categories that have been matched.
         "Swearing",
         "Interruptions"
      ],
       "MatchedDetails" :{ 
          "Swearing" :{ 
             "PointsOfInterest" :[ 
               { 
                   "BeginOffsetMillis" :0,  //The swearing is called out with the beginning and end offset.
                   "EndOffsetMillis" :300
               },
               { 
                   "BeginOffsetMillis" :360,
                   "EndOffsetMillis" :500
               }
            ]
         },
          "Interruptions" :{ 
             "PointsOfInterest" :[ 
               { 
                   "BeginOffsetMillis" :0,  //The interruptions are called out with the beginning and end offset.
                   "EndOffsetMillis" :500
               },
               { 
                   "BeginOffsetMillis" :360,
                   "EndOffsetMillis" :500
               }
            ]
         }
      }
   },
    "ConversationCharacteristics" :{ 
       "TotalConversationDurationMillis" :7060,
       "NonTalkTime" :{ 
          "TotalTimeMillis" :172,
          "Instances" :[ 
            { 
                "BeginOffsetMillis" :3,
                "EndOffsetMillis" :60,
                "DurationMillis" :57
            },
            { 
                "BeginOffsetMillis" :45,
                "EndOffsetMillis" :160,
                "DurationMillis" :115
            }
         ]
      },
       "TalkTime" :{ 
          "TotalTimeMillis" :90000,
          "DetailsByParticipant" :{ 
             "55555555-5555-5555-5555-55555555555" :{ 
                "TotalTimeMillis" :45000
            },
             "33333333" :{ 
                "TotalTimeMillis" :45000
            }
         }
      },
       "TalkSpeed" :{ 
          "DetailsByParticipant" :{ 
             "55555555-5555-5555-5555-55555555555" :{ 
                "AverageWordsPerMinute" :34
            },
             "33333333" :{ 
                "AverageWordsPerMinute" :40
            }
         }
      },
       "Interruptions" :{ 
          "TotalCount" :2,
          "TotalTimeMillis" :34,
          "InterruptionsByInterrupter" :{ 
             "55555555-5555-5555-5555-55555555555" :[ 
               { 
                   "BeginOffsetMillis" :3,
                   "EndOffsetMillis" :34,
                   "DurationMillis" :31  //This is how many milliseconds the agent talked over the customer.
               },
               { 
                   "BeginOffsetMillis" :67,
                   "EndOffsetMillis" :70,
                   "DurationMillis" :3
               }
            ]
         }
      },
       "Sentiment" :{ 
          "OverallSentiment" :{ 
             "55555555-5555-5555-5555-55555555555" :3,  //The agent's overall sentiment score.
             "33333333" :4.2   //The customer's overall sentiment score.
         },
          "SentimentByPeriod" :{ 
             "QUARTER" :{ 
                "55555555-5555-5555-5555-55555555555" :[ 
                  { 
                      "BeginOffsetMillis" :0,
                      "EndOffsetMillis" :100,
                      "Score" :3.0
                  },
                  { 
                      "BeginOffsetMillis" :100,
                      "EndOffsetMillis" :200,
                      "Score" :3.1
                  },
                  { 
                      "BeginOffsetMillis" :200,
                      "EndOffsetMillis" :300,
                      "Score" :3.6
                  },
                  { 
                      "BeginOffsetMillis" :300,
                      "EndOffsetMillis" :400,
                      "Score" :3.1
                  }
               ],
                "33333333" :[ 
                  { 
                      "BeginOffsetMillis" :0,
                      "EndOffsetMillis" :100,
                      "Score" :3.1
                  },
                  { 
                      "BeginOffsetMillis" :100,
                      "EndOffsetMillis" :200,
                      "Score" :3.2
                  },
                  { 
                      "BeginOffsetMillis" :200,
                      "EndOffsetMillis" :300,
                      "Score" :3.6
                  },
                  { 
                      "BeginOffsetMillis" :300,
                      "EndOffsetMillis" :400,
                      "Score" :3.6
                  }
               ]
            }
         }
      }
   }
 }
```

## Example redacted file<a name="example-redacted-file"></a>

This section shows an example redacted file\. It's a twin of the original analyzed file\. The only difference is that sensitive data are redacted\. 

```
{
    "Participants" :[ 
      { 
          "ParticipantId" :"55555555-5555-5555-5555-55555555555",
          "ParticipantRole" :"AGENT"
      },
      { 
          "ParticipantId" :"33333333",
          "ParticipantRole" :"CUSTOMER"
      }
   ],
    "Channel" :"VOICE",
    "AccountId" :"BBBBBBBBBBB",
    "Version": "1.0.0",
    "JobStatus" :"COMPLETED",
    "LanguageCode" :"en-US",
    "CustomModels" :[ 
      { 
          "Type" :"TRANSCRIPTION_VOCABULARY",
          "Name" :"MostCommonKeywordsTranscriptionV1"
      },
      { 
          "Type" :"TEXT_ANALYSIS_ENTITIES",
          "Name" :"Top100EntitiesV2"
      }
   ],
   "ContentMetadata" : {
        "RedactionTypes": [“PII”], //It says "PII" even though the redacted content could be other sensitive data such as credit card number.
        "Output": “Redacted"
   },
    "CustomerMetadata" :{ 
       "InputS3Uri" :"s3://connect-cccccccccccccc/connect/poc-1/CallRecordings/2019/07/22/dddddddd-dddd-dddd-dddd-dddddddddddd_20190322T23:23_UTC.wav",
       "ContactId" :"11111111-1111-1111-1111-11111111111",
       "InstanceId" :"eeeeeee-eeee-eeee-eeee-eeeeeeeeeeee"
   },
    "Transcript" :[ 
      { 
          "ParticipantId" :"55555555-5555-5555-5555-55555555555",
          "Id" :"tttttttt-tttt-tttt-tttt-tttttttt",
          "Content": "Hello, my name is Jane, may I have your email id?",
          "BeginOffsetMillis" :0,
          "EndOffsetMillis" :300,
          "Sentiment" :"NEUTRAL",
           "LoudnessScore":[
            40.5,
            55.0,
            59.3
         ],
      },
      { 
          "ParticipantId" :"33333333",
          "Id" :"sssssssss-ssss-ssss-ssss-sssssssss",
          "Content": "My email id is [PII].",  //This shows that the customer's email ID has been redacted.
          "BeginOffsetMillis" :500,
          "EndOffsetMillis" :945,
          "Sentiment" :"NEGATIVE",
          "LoudnessScore":[
            40.5,
            55.0,
            59.3
         ],
          "Redaction"  :{    
               "RedactedTimestamps"  :[    
                  {    
                     "BeginOffsetMillis"  :  900, 
                     "EndOffsetMillis"  :  944, 
                  } 
               ], 
      },
      {
        "ParticipantId": "33333333",
        "Id": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaaa",
        "Content": "Hi, I'm having trouble submitting the application, number [PII] on the portal.
                   I tried but couldn't connect to my POC on the portal.
                   So, I'm calling on this toll free number."
        "BeginOffsetMillis": 1500,
        "EndOffsetMillis": 1945,
        "Sentiment": "NEGATIVE",
        "LoudnessScore":[
            40.5,
            55.0,
            59.3
         ],
        "Redaction": {
                "RedactedTimestamps": [{
                        "BeginOffsetMillis": 1610,
                        "EndOffsetMillis": 1700  
                }]
        },
        "IssuesDetected": [{
               "CharacterOffsets": {
                        "BeginOffsetChar": 0, 
                        "EndOffsetChar": 78   
                    },
                  "Text": "Hi, I'm having trouble submitting the application, number [PII] on the portal.
                   I tried but couldn't connect to my POC on the portal.
                   So, I'm calling on this toll free number."
                  }]         
    }
  ],
    "Categories" :{ 
       "MatchedCategories" :[ 
         "Greeting",
         "Interruptions"
      ],
       "MatchedDetails" :{ 
          "Greeting" :{ 
             "PointsOfInterest" :[ 
               { 
                   "BeginOffsetMillis" :0,
                   "EndOffsetMillis" :300
               },
               { 
                   "BeginOffsetMillis" :360,
                   "EndOffsetMillis" :500
               }
            ]
         },
          "Interruptions" :{ 
             "PointsOfInterest" :[ 
               { 
                   "BeginOffsetMillis" :0,
                   "EndOffsetMillis" :500
               },
               { 
                   "BeginOffsetMillis" :360,
                   "EndOffsetMillis" :500
               }
            ]
         }
      }
   },
    "ConversationCharacteristics" :{ 
       "TotalConversationDurationMillis" :7060,
       "NonTalkTime" :{ 
          "TotalTimeMillis" :172,
          "Instances" :[ 
            { 
                "BeginOffsetMillis" :3,
                "EndOffsetMillis" :60,
                "DurationMillis" :57
            },
            { 
                "BeginOffsetMillis" :45,
                "EndOffsetMillis" :160,
                "DurationMillis" :115
            }
         ]
      },
       "TalkTime" :{ 
          "TotalTimeMillis" :90000,
          "DetailsByParticipant" :{ 
             "55555555-5555-5555-5555-55555555555" :{ 
                "TotalTimeMillis" :45000
            },
             "33333333" :{ 
                "TotalTimeMillis" :45000
            }
         }
      },
       "TalkSpeed" :{ 
          "DetailsByParticipant" :{ 
             "55555555-5555-5555-5555-55555555555" :{ 
                "AverageWordsPerMinute" :34
            },
             "33333333" :{ 
                "AverageWordsPerMinute" :40
            }
         }
      },
       "Interruptions" :{ 
          "TotalCount" :2,
          "TotalTimeMillis" :34,
          "InterruptionsByInterrupter" :{ 
             "55555555-5555-5555-5555-55555555555" :[ 
               { 
                   "BeginOffsetMillis" :3,
                   "EndOffsetMillis" :34,
                   "DurationMillis" :31
               },
               { 
                   "BeginOffsetMillis" :67,
                   "EndOffsetMillis" :70,
                   "DurationMillis" :3
               }
            ]
         }
      },
       "Sentiment" :{ 
          "OverallSentiment" :{ 
             "55555555-5555-5555-5555-55555555555" :3,
             "33333333" :4.2
         },
          "SentimentByPeriod" :{ 
             "QUARTER" :{ 
                "55555555-5555-5555-5555-55555555555" :[ 
                  { 
                      "BeginOffsetMillis" :0,
                      "EndOffsetMillis" :100,
                      "Score" :3.0
                  },
                  { 
                      "BeginOffsetMillis" :100,
                      "EndOffsetMillis" :200,
                      "Score" :3.1
                  },
                  { 
                      "BeginOffsetMillis" :200,
                      "EndOffsetMillis" :300,
                      "Score" :3.6
                  },
                  { 
                      "BeginOffsetMillis" :300,
                      "EndOffsetMillis" :400,
                      "Score" :3.1
                  }
               ],
                "33333333" :[ 
                  { 
                      "BeginOffsetMillis" :0,
                      "EndOffsetMillis" :100,
                      "Score" :3.1
                  },
                  { 
                      "BeginOffsetMillis" :100,
                      "EndOffsetMillis" :200,
                      "Score" :3.2
                  },
                  { 
                      "BeginOffsetMillis" :200,
                      "EndOffsetMillis" :300,
                      "Score" :3.6
                  },
                  { 
                      "BeginOffsetMillis" :300,
                      "EndOffsetMillis" :400,
                      "Score" :3.6
                  }
               ]
            }
         }
      }
   }
 }
```