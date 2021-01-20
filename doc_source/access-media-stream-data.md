# How to access Kinesis Video Streams data<a name="access-media-stream-data"></a>

You must have developer skills to work with Kinesis Video Streams data\. Use the steps and code samples in this section to interact with the customer audio data sent to Kinesis Video Streams\.

## Get started with a sample<a name="get-started-media-stream"></a>

There's an example project on GitHub to help you to get started using Amazon Connect live audio streaming and real\-time transcription using Amazon Transcribe\. See [Amazon Connect Real\-time Transcription Lambda](https://github.com/amazon-connect/amazon-connect-realtime-transcription)\.

This project provides a code example and a fully functional Lambda function\. They help you get started capturing and transcribing Amazon Connect phone calls using Kinesis Video Streams and Amazon Transcribe\. 

You can use the Lambda function in this project to create other solutions, such as: 
+ Capturing audio in the IVR\.
+ Providing real\-time transcription to agents\.
+ Creating a voicemail solution for Amazon Connect\.

## Build your own implementation<a name="get-started-media-stream-scratch"></a>

You may want to implement a solution other than the one provided by the previously\-described sample\. If so, this section describes how to make the proper API calls against the Kinesis Video Streams so you can build your own solution from scratch\. 

1. Go to [this GitHub page](https://github.com/amazon-connect/amazon-connect-realtime-transcription), and read about the Amazon Connect Real\-time Transcription Lambda project\.

1. Choose the **deployment** folder, and download the **cloudformation\.template**\.

1. Use the following example Java classes, which are built on top of the Kinesis video parser library using the AWS SDK for Java\.
   + **LMSDemo**— is a class with a main method that invokes LMSExample\.
   + **LMSExample**— is similar to the examples provided in the Kinesis Video Streams Parser library\. It gets media from the specified Kinesis Video Streams with the specified fragment number\. This code sample includes frame processing to separate the tracks\.
   + **LMSFrameProcessor**— is invoked by LMSExample to save data from Kinesis Video Streams to the specified output stream\. Use a file output stream to save the output to a file\. This code sample also includes frame processing to separate the tracks\.

1. Use [Audacity](https://www.audacityteam.org), or other audio tool, to import the \.raw audio file, which is in a 16\-bit signed PCM Mono format\.

### Code samples to access Kinesis Video Streams data<a name="media-streaming-code-samples"></a>

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
    private final OutputStream outputStreamFromCustomer;
    private final OutputStream outputStreamToCustomer;
    private final String fragmentNumber;

    public LMSExample(Regions region,
                      String streamName,
                      String fragmentNumber,
                      AWSCredentialsProvider credentialsProvider,
                      OutputStream outputStreamFromCustomer,
                      OutputStream outputStreamToCustomer) throws IOException {
        super(region, credentialsProvider, streamName);
        this.streamOps = new StreamOps(region,  streamName, credentialsProvider);
        this.executorService = Executors.newFixedThreadPool(2);
        this.outputStreamFromCustomer = outputStreamFromCustomer;
        this.outputStreamToCustomer = outputStreamToCustomer;
        this.fragmentNumber = fragmentNumber;
    }

    public void execute () throws InterruptedException, IOException {
        getMediaProcessingArguments = GetMediaProcessingArguments.create(outputStreamFromCustomer, outputStreamToCustomer);
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

        public static GetMediaProcessingArguments create(OutputStream outputStreamFromCustomer, OutputStream outputStreamToCustomer) throws IOException {
            //Fragment metadata visitor to extract Kinesis Video fragment metadata from the GetMedia stream.
            FragmentMetadataVisitor fragmentMetadataVisitor = FragmentMetadataVisitor.create();

            //A visitor used to log as the GetMedia stream is processed.
            LogVisitor logVisitor = new LogVisitor(fragmentMetadataVisitor);

            //A composite visitor to encapsulate the three visitors.
            FrameVisitor frameVisitor =
                    FrameVisitor.create(LMSFrameProcessor.create(outputStreamFromCustomer, outputStreamToCustomer, fragmentMetadataVisitor));

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
import com.amazonaws.kinesisvideo.parser.utilities.FragmentMetadataVisitor;
import com.amazonaws.kinesisvideo.parser.utilities.MkvTrackMetadata;

import java.io.IOException;
import java.io.OutputStream;
import java.nio.ByteBuffer;

public class LMSFrameProcessor implements FrameVisitor.FrameProcessor {

    private OutputStream outputStreamFromCustomer;
    private OutputStream outputStreamToCustomer;
    private FragmentMetadataVisitor fragmentMetadataVisitor;

    protected LMSFrameProcessor(OutputStream outputStreamFromCustomer, OutputStream outputStreamToCustomer, FragmentMetadataVisitor fragmentMetadataVisitor) {
        this.outputStreamFromCustomer = outputStreamFromCustomer;
        this.outputStreamToCustomer = outputStreamToCustomer;
    }

    public static LMSFrameProcessor create(OutputStream outputStreamFromCustomer, OutputStream outputStreamToCustomer, FragmentMetadataVisitor fragmentMetadataVisitor) {
        return new LMSFrameProcessor(outputStreamFromCustomer, outputStreamToCustomer, fragmentMetadataVisitor);
    }

    @Override
    public void process(Frame frame, MkvTrackMetadata trackMetadata) {
        saveToOutPutStream(frame);
    }

    private void saveToOutPutStream(final Frame frame) {
        ByteBuffer frameBuffer = frame.getFrameData();
        long trackNumber = frame.getTrackNumber();
        MkvTrackMetadata metadata = fragmentMetadataVisitor.getMkvTrackMetadata(trackNumber);
        String trackName = metadata.getTrackName();

        try {
            byte[] frameBytes = new byte[frameBuffer.remaining()];
            frameBuffer.get(frameBytes);
            if (Strings.isNullOrEmpty(trackName) || "AUDIO_FROM_CUSTOMER".equals(trackName)) {
              outputStreamFromCustomer.write(frameBytes);
            } else if ("AUDIO_FROM_CUSTOMER".equals(trackName)) {
              outputStreamToCustomer.write(frameBytes);
            } else {
              // Unknown track name. Not writing to output stream.
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```