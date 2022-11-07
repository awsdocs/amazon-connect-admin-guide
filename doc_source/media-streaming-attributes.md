# Contact attributes for live media streaming<a name="media-streaming-attributes"></a>

The attributes are displayed when you select **Media streams** for the **Type** in a flow block that supports attributes, such as the **Start media streaming** block\. They include the following:

Customer audio stream ARN  
The ARN of the Kinesis video stream that includes the customer data to reference\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StreamARN

Customer audio start timestamp  
The time at which the customer audio stream started\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StartTimestamp

Customer audio stop timestamp  
The time at which the customer audio stream stopped\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StopTimestamp

Customer audio start fragment number  
The number that identifies the Kinesis Video Streams fragment in which the customer audio stream started\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StartFragmentNumber

For more information about Amazon Kinesis Video Streams fragments, see [Fragment](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/API_reader_Fragment.html) in the * Amazon Kinesis Video Streams Developer Guide*\.