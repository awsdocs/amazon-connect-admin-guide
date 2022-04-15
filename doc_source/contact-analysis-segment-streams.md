# Use streaming for real\-time contact analysis<a name="contact-analysis-segment-streams"></a>

Real\-time contact analysis segment streams enable you to access Contact Lens analytics in near real\-time\. Real\-time streaming overcomes the scaling limitations of existing [real\-time analytics API](contact-lens-api.md)\. It also provides access to a data segment called `Utterance` that allows you to access partial transcripts\. This enables you to meet ultra\-low latency requirements to assist agents on live calls\. 

This section explains how to integrate with Amazon Kinesis Data Streams for real\-time streaming\.

Through real\-time streaming, you can receive the following event types: 
+ STARTED events published at the beginning of a real\-time contact analysis session\.
+ SEGMENTS events published during the real\-time contact analysis sessions\. These events contain a list of segments with analyzed information\.
+ COMPLETED or FAILED events published at the end of a real\-time contact analysis session\.

**Topics**
+ [Enable real\-time contact analysis segment streams](enable-contact-analysis-segment-streams.md)
+ [Real\-time contact analysis segment streams data model](real-time-contact-analysis-segment-streams-data-model.md)
+ [Sample real\-time contact analysis segment stream](sample-real-time-contact-analysis-segment-stream.md)