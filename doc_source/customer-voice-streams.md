# Capture Customer Audio: Live Media Streaming<a name="customer-voice-streams"></a>

In Amazon Connect, you can capture the customer audio during an interaction with your contact center by sending the audio to a Kinesis Video Stream\. 
+ All customer audio is captured in the stream from the customer, starting when the **Start media streaming** block is invoked in a contact flow\.
+ Customer audio is captured for the entire interaction\. This includes when the customer is interacting with an Amazon Lex bot that is used in your contact flow, and when the customer on hold\.

The customer audio is stored in Kinesis for the time defined by your retention settings\. You can use the customer audio streams to perform analysis on the audio to determine customer sentiment, use the audio for training purposes, or to later review the audio to identify and flag abusive callers\. Only customer audio is sent to Kinesis Video Streams\. Audio sent to Kinesis uses a sampling rate of 8 Khz\.

When you enable media streaming in Amazon Connect, one Kinesis Video stream is used per call\. The default Kinesis service limit for the **Number of Video Streams** is 1000 streams per AWS account\. To make sure that there are enough streams available for all calls in your contact center, set the limit for the **Number of Video Streams** to a value greater than the number of the maximum concurrent active calls for your instance\. If you have more than one instance for your AWS account, increase the **Number of Video Streams** limit to a number greater than the concurrent active calls for all of your instances combined\.

**Topics**
+ [Enable Live Media Streaming](enable-live-media-streams.md)
+ [Example Contact Flow for Testing Live Media Streaming](use-media-streams-blocks.md)
+ [Live Media Streaming Contact Attributes](media-streaming-attributes.md)
+ [Access Kinesis Video Stream Data](access-media-stream-data.md)