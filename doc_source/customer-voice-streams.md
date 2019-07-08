# Capture Customer Audio: Live Media Streaming<a name="customer-voice-streams"></a>

In Amazon Connect, you can capture the customer audio during an interaction with your contact center by sending the audio to a Kinesis Video Stream\. All customer audio is captured in the stream from the customer, starting when the **Start media streaming** block is invoked in a contact flow\. Customer audio is captured for the entire interaction, including when the customer is interacting with an Amazon Lex bot that is used in your contact flow, and when the customer on hold\. 

The customer audio is stored in Kinesis for the time defined by your retention settings\. You can use the customer audio streams to perform analysis on the audio to determine customer sentiment, use the audio for training purposes, or to later review the audio to identify and flag abusive callers\. Only customer audio is sent to Kinesis Video Streams\. Audio sent to Kinesis uses a sampling rate of 8 Khz\.

When you enable media streaming in Amazon Connect, one Kinesis Video stream is used per call\. The default Kinesis service limit for the **Number of Video Streams** is 100 streams per AWS account\. To make sure that there are enough streams available for all calls in your contact center, set the limit for the **Number of Video Streams** to a value greater than the number of the maximum concurrent active calls for your instance\. If you have more than one instance for your AWS account, increase the **Number of Video Streams** limit to a number greater than the concurrent active calls for all of your instances combined\.

## Enable Live Media Streaming<a name="enable-live-media-streams"></a>

Live media streaming \(customer audio streams\) is not enabled by default\. You can enable customer audio streams from the settings page for your instance\.

**To enable live media streaming**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the instance alias for the instance from the **Instance Alias** column\.

1. In the navigation pane, choose **Data storage**\.

1. Under **Live media streaming**, choose **Edit**\. Choose **Enable live media streaming**\.

1. Enter a prefix for the Kinesis Video Stream created for your customer audio\. This prefix makes it easier for you to identify the stream with the data\.

1. Choose the KMS master key to use to encrypt the data sent to Kinesis\.

1. Specify a number and unit for the **Data retention period**\. If you select **No data retention**, data is not retained and can be used only for immediate consumption\.

1. Choose **Save** under **Live media streaming**, and then choose **Save** at the bottom of the page\.

## Example Contact Flow for Testing Live Media Streaming<a name="use-media-streams-blocks"></a>

In a contact flow, add a **Start media streaming** block in the flow at the point where you want to enable customer audio streaming\. Connect the **Success** branch to the rest of your flow\. When you want to stop customer media streaming, add a **Stop media streaming** block to the flow\. Customer audio is captured until a **Stop media streaming** block is invoked, even if the contact is passed to another contact flow\.

Use the contact attributes for media streaming in your contact flow so that the CTR includes the attributes\. You can then view the CTR to determine the media streaming data associated with a specific contact\. You can also pass the attributes to an AWS Lambda function\.

The following example contact flow demonstrates using media streaming with attributes for testing purposes\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/media-streaming-flow.png)

After the audio is successfully streamed to Kinesis Video Streams, the contact attributes are populated from the **Invoke AWS Lambda function** block\. You can use the attributes to identify the location in the stream where the customer audio starts\.

## Live Media Streaming Contact Attributes<a name="media-streaming-attributes"></a>

The attributes, displayed when you select **Media streams** for the **Type** in a contact flow block that supports attributes include the following:

Customer audio stream ARN  
The ARN of the Kinesis Video stream that includes the customer data to reference\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StreamARN

Customer audio start timestamp  
The time at which the customer audio stream started\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StartTimestamp

Customer audio stop timestamp  
The time at which the customer audio stream stopped\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StopTimestamp

Customer audio start fragment number  
The number that identifies the Kinesis Video Streams fragment in which the customer audio stream started\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StartPosition

Customer audio stop fragment number  
The number that identifies the Kinesis Video Streams fragment in which the customer audio stream stopped\.  
**JSONPath format: **$\.MediaStreams\.Customer\.Audio\.StopPosition

For more information about Amazon Kinesis Video Streams fragments, see [Fragment](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/API_reader_Fragment.html) in the * Amazon Kinesis Video Streams Developer Guide*\.

## How to Access Kinesis Video Stream Data<a name="access-media-stream-data"></a>

Use the steps and code samples in this section to interact with the customer audio data sent to Kinesis Video Streams\.

First, download the [Kinesis Video parser library](https://github.com/aws/amazon-kinesis-video-streams-parser-library/archive/v1.0.3.zip)\.

Next, use the following example Java classes, which are built on top of the Kinesis video parser library using the AWS SDK for Java\.
+ **LMSDemo**—is a class with a main method that invokes LMSExample\.
+ **LMSExample**—is similar to the examples provided in the KVS Parser library that gets media from the specified Kinesis Video Stream with the specified fragment number\.
+ **LMSFrameProcessor**—is invoked by LMSExample to save data from Kinesis Video Streams to the specified output stream\. Use a file output stream to save the output to a file\.

Then, use Audacity \(https://www\.audacityteam\.org/\), or other audio tool, to import the \.raw audio file, which is a 16\-bit signed PCM Mono format\.

### Code Samples to Access Kinesis Video Stream Data<a name="media-streaming-code-samples"></a>

#### LMSDemo\.java<a name="lasdemo-java"></a>

```
package com.amazonaws.kinesisvideo.parser.demo;

import com.amazonaws.auth.AWSSessionCredentials;
import com.amazonaws.auth.AWSSessionCredentialsProvider;
import com.amazonaws.kinesisvideo.parser.examples.LMSExample;
import com.amazonaws.regions.Regions;


import java.io.FileOutputStream;
import java.io.IOException;

public class LMSDemo {

    public static void main(String args[]) throws InterruptedException, IOException {
        LMSExample example = new LMSExample(Regions.US_WEST_2,
                                            "<<StreamName>>",
                                            "<<FragmentNumber>>",
                             new AWSSessionCredentialsProvider() {
                                                @Override
                             public AWSSessionCredentials getCredentials() {
                                 return new AWSSessionCredentials() {
                                                        @Override
                             public String getSessionToken() {
                                 return "<<AWSSessionToken>>";
                                                        }

                                                        @Override
                             public String getAWSAccessKeyId() {
                                 return "<<AWSAccessKey>>";
                                                        }

                                                        @Override
                             public String getAWSSecretKey() {
                                 return "<<AWSSecretKey>>";
                                                        }
                                                    };
                                                }

                                                @Override
                             public void refresh() {

                                                }
                                            },
                             new FileOutputStream("<<FileName>>.raw"));

                                 example.execute();
    }

}
```

#### LMSExample\.java<a name="lasexample-java"></a>

```
package com.amazonaws.kinesisvideo.parser.examples;

import com.amazonaws.auth.AWSCredentialsProvider;
import com.amazonaws.kinesisvideo.parser.ebml.MkvTypeInfos;
import com.amazonaws.kinesisvideo.parser.mkv.MkvDataElement;
import com.amazonaws.kinesisvideo.parser.mkv.MkvElementVisitException;
import com.amazonaws.kinesisvideo.parser.mkv.MkvElementVisitor;
import com.amazonaws.kinesisvideo.parser.mkv.MkvEndMasterElement;
import com.amazonaws.kinesisvideo.parser.mkv.MkvStartMasterElement;
import com.amazonaws.kinesisvideo.parser.utilities.FragmentMetadataVisitor;
import com.amazonaws.kinesisvideo.parser.utilities.FrameVisitor;
import com.amazonaws.kinesisvideo.parser.utilities.LMSFrameProcessor;
import com.amazonaws.regions.Regions;
import com.amazonaws.services.kinesisvideo.model.StartSelector;
import com.amazonaws.services.kinesisvideo.model.StartSelectorType;

import java.io.Closeable;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.io.PipedInputStream;
import java.io.PipedOutputStream;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class LMSExample extends KinesisVideoCommon {

    private final ExecutorService executorService;
    private GetMediaProcessingArguments getMediaProcessingArguments;
    private final StreamOps streamOps;
    private final OutputStream outputStream;
    private final String fragmentNumber;

    public LMSExample(Regions region,
                      String streamName,
                      String fragmentNumber,
                      AWSCredentialsProvider credentialsProvider,
                      OutputStream outputStream) throws IOException {
        super(region, credentialsProvider, streamName);
        this.streamOps = new StreamOps(region,  streamName, credentialsProvider);
        this.executorService = Executors.newFixedThreadPool(2);
        this.outputStream = outputStream;
        this.fragmentNumber = fragmentNumber;
    }

    public void execute () throws InterruptedException, IOException {
        getMediaProcessingArguments = GetMediaProcessingArguments.create(outputStream);
        try (GetMediaProcessingArguments getMediaProcessingArgumentsLocal = getMediaProcessingArguments) {
            //Start a GetMedia worker to read and process data from the Kinesis Video Stream.
            GetMediaWorker getMediaWorker = GetMediaWorker.create(getRegion(),
            getCredentialsProvider(),
            getStreamName(),
            new StartSelector().withStartSelectorType(StartSelectorType.FRAGMENT_NUMBER).withAfterFragmentNumber(fragmentNumber),
            streamOps.amazonKinesisVideo,
            getMediaProcessingArgumentsLocal.getFrameVisitor());
            executorService.submit(getMediaWorker);

            //Wait for the workers to finish.
            executorService.shutdown();
            executorService.awaitTermination(120, TimeUnit.SECONDS);
            if (!executorService.isTerminated()) {
                System.out.println("Shutting down executor service by force");
                executorService.shutdownNow();
            } else {
                System.out.println("Executor service is shutdown");
            }
        } finally {
            outputStream.close();
        }

    }

    private static class LogVisitor extends MkvElementVisitor {
        private final FragmentMetadataVisitor fragmentMetadataVisitor;

        private LogVisitor(FragmentMetadataVisitor fragmentMetadataVisitor) {
            this.fragmentMetadataVisitor = fragmentMetadataVisitor;
        }

        public long getFragmentCount() {
            return fragmentCount;
        }

        private long fragmentCount = 0;

        @Override
        public void visit(MkvStartMasterElement startMasterElement) throws MkvElementVisitException {
            if (MkvTypeInfos.EBML.equals(startMasterElement.getElementMetaData().getTypeInfo())) {
                fragmentCount++;
                System.out.println("Start of segment");
            }
        }

        @Override
        public void visit(MkvEndMasterElement endMasterElement) throws MkvElementVisitException {
            if (MkvTypeInfos.SEGMENT.equals(endMasterElement.getElementMetaData().getTypeInfo())) {
                System.out.println("End of segment");
                                      
            }
        }

        @Override
        public void visit(MkvDataElement dataElement) throws MkvElementVisitException {
        }
    }

    private static class GetMediaProcessingArguments implements Closeable {

        public FrameVisitor getFrameVisitor() {
            return frameVisitor;
        }

        private final FrameVisitor frameVisitor;

        public GetMediaProcessingArguments(FrameVisitor frameVisitor) {
            this.frameVisitor = frameVisitor;
        }

        public static GetMediaProcessingArguments create(OutputStream outPutStream) throws IOException {
            //Fragment metadata visitor to extract Kinesis Video fragment metadata from the GetMedia stream.
            FragmentMetadataVisitor fragmentMetadataVisitor = FragmentMetadataVisitor.create();

            //A visitor used to log as the GetMedia stream is processed.
            LogVisitor logVisitor = new LogVisitor(fragmentMetadataVisitor);

            //A composite visitor to encapsulate the three visitors.
            FrameVisitor frameVisitor =
                    FrameVisitor.create(LMSFrameProcessor.create(outPutStream));

            return new GetMediaProcessingArguments(frameVisitor);
        }

        @Override
        public void close() throws IOException {

        }

    }
}
```

#### LMSFrameProcessor\.java<a name="lasframeprocessor-java"></a>

```
package com.amazonaws.kinesisvideo.parser.utilities;

import com.amazonaws.kinesisvideo.parser.mkv.Frame;

import java.io.IOException;
import java.io.OutputStream;
import java.nio.ByteBuffer;

public class LMSFrameProcessor implements FrameVisitor.FrameProcessor {

    private OutputStream outputStream;


    protected LMSFrameProcessor(OutputStream outputStream) {
        this.outputStream = outputStream;
    }

    public static LMSFrameProcessor create(OutputStream outputStream) {
        return new LMSFrameProcessor(outputStream);
    }

    @Override
    public void process(Frame frame, MkvTrackMetadata trackMetadata) {
        saveToOutPutStream(frame);
    }

    private void saveToOutPutStream(final Frame frame) {
        ByteBuffer frameBuffer = frame.getFrameData();
        try {
            byte[] frameBytes = new byte[frameBuffer.remaining()];
            frameBuffer.get(frameBytes);
            outputStream.write(frameBytes);

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```