# Capture Customer Audio: Live Media Streaming<a name="customer-voice-streams"></a>

In Amazon Connect, you can capture customer audio during an interaction with your contact center by sending the audio to a Kinesis video stream\. Depending on your settings, audio can be captured for the entire interaction—until the interaction with the agent is complete—or only one direction: 
+ What the customer hears, including what the agent says and system prompts\.
+ What the customer says, including when they are on hold\.

The customer audio streams also include interactions with an Amazon Lex bot, if you're using one in your contact flow\. 

You can perform analysis on the audio streams to determine customer sentiment, use the audio for training purposes, or to later review the audio to identify and flag abusive callers\.

**Topics**
+ [Plan for Live Media Streaming](plan-live-media-streams.md)
+ [Enable Live Media Streaming](enable-live-media-streams.md)
+ [Access Kinesis Video Streams Data](access-media-stream-data.md)
+ [Test Live Media Streaming](use-media-streams-blocks.md)
+ [Contact Attributes for Live Media Streaming](media-streaming-attributes.md)