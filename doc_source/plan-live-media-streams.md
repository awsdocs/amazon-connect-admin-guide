# Plan for Live Media Streaming<a name="plan-live-media-streams"></a>

You can send all audio to and from the customer to Kinesis Video Streams\. Media streaming leverages Kinesis Video Streams multi\-track support so that what the customer says is on a separate track from what the customer hears\. 

Audio sent to Kinesis uses a sampling rate of 8 Khz\.

## Do You Need to Increase Your Service Limits?<a name="create-streams-service-limit"></a>

When you enable media streaming in Amazon Connect, one Kinesis video stream is used per active call\. By default we allocate 50 streams to your account\. We automatically create additional streams as needed to keep pace with active calls, unless your account reaches the Kinesis Video Streams service limit\.

Check out the [default Kinesis service limit](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/limits.html) for number of streams per account for your region \(see the limit for the **CreateStream** API\)\.

To make sure that there are enough streams available for all calls in your contact center, the value of the **CreateStream** API needs to be greater than the number of the maximum concurrent active calls for your instance\.

If you have more than one instance for your AWS account, your **CreateStream** limit should be a number greater than the concurrent active calls for all of your instances combined\.

To request an increase to your service limit, in the AWS Support Center, choose **Create Case** and then choose **Service Limit Increase**\.

**Tip**  
We make sure that **PutMedia** requests always stay within the 5 TPS limit\. You don't need to request an increase\.

## How Long Do You Need to Store Audio?<a name="storing-audio-streams"></a>

Customer audio is stored in Kinesis for the time defined by your retention settings in an Amazon Connect instance\. For instructions for setting this value, see [Enable Live Media Streaming in Your Instance](enable-live-media-streams.md)\.

## Who Requires IAM Permissions to Retrieve Data?<a name="perms-audio-streams"></a>

If your business is using IAM policies and permissions, the IAM admin will need to grant permissions to people who are going to retrieve data from Kinesis Video Streams\. They'll need to grant them full access permissions for Kinesis Video Streams and AWS Key Management Service\.