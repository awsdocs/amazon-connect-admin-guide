# Plan for live media streaming<a name="plan-live-media-streams"></a>

You can send all audio to and from the customer to Kinesis Video Streams\. Media streaming leverages Kinesis Video Streams multi\-track support so that what the customer says is on a separate track from what the customer hears\. 

Audio sent to Kinesis uses a sampling rate of 8 Khz\.

## Do you need to increase your service quotas?<a name="create-streams-service-limit"></a>

When you enable media streaming in Amazon Connect, one Kinesis video stream is used per active call\. By default we allocate 50 streams per instance to your account\. We automatically create additional streams as needed to keep pace with active calls, unless your account reaches the [Kinesis Video Streams service quota](https://docs.aws.amazon.com/streams/latest/dev/service-sizes-and-limits.html)\.

Contact AWS Support to request an increase to **Number of Streams**\.

To request an increase to your service quota, in the AWS Support Center, choose **Create Case** and then choose **Service Quota Increase**\.

**Tip**  
We make sure that **PutMedia** requests always stay within the 5 TPS quota\. You don't need to request an increase\.

## How long do you need to store audio?<a name="storing-audio-streams"></a>

Customer audio is stored in Kinesis for the time defined by your retention settings in an Amazon Connect instance\. For instructions for setting this value, see [Enable live media streaming in your instance](enable-live-media-streams.md)\.

**Tip**  
If you want to use the audio streaming feature, you need to retain the streams that are created by Amazon Connect\. Don't delete them, unless you're going to stop using the streaming feature\.

## Do you need to change the audio streams?<a name="changing-audio-streams"></a>

We recommend that you refrain from modifying the streams\. Doing so can cause unexpected behavior\.

## Who requires IAM permissions to retrieve data?<a name="perms-audio-streams"></a>

If your business is using IAM permissions, your AWS admin will need to grant permissions to people who are going to retrieve data from Kinesis Video Streams\. They'll need to grant them full access permissions for Kinesis Video Streams and AWS Key Management Service\.