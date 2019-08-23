# How to Access Kinesis Video Stream Data<a name="access-media-stream-data"></a>

You must have developer skills to access Kinesis video stream data\. Use the steps and code samples in this section to interact with the customer audio data sent to Kinesis Video Streams\.

First, download the [Kinesis Video parser library](https://github.com/aws/amazon-kinesis-video-streams-parser-library/archive/v1.0.3.zip)\. This library includes an easy\-to\-use set of tools can use in Java applications to consume the MKV data in a Kinesis video stream\. To learn more, see [Kinesis Video Stream Parser Library](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/parser-library.html)\.

Next, use the following example Java classes, which are built on top of the Kinesis video parser library using the AWS SDK for Java\.
+ **LMSDemo**—is a class with a main method that invokes LMSExample\.
+ **LMSExample**—is similar to the examples provided in the KVS Parser library that gets media from the specified Kinesis Video Stream with the specified fragment number\.
+ **LMSFrameProcessor**—is invoked by LMSExample to save data from Kinesis Video Streams to the specified output stream\. Use a file output stream to save the output to a file\.

Then, use Audacity \(https://www\.audacityteam\.org/\), or other audio tool, to import the \.raw audio file, which is a 16\-bit signed PCM Mono format\.

## Code Samples to Access Kinesis Video Stream Data<a name="media-streaming-code-samples"></a>

### LMSDemo\.java<a name="lasdemo-java"></a>

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

### LMSExample\.java<a name="lasexample-java"></a>

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

### LMSFrameProcessor\.java<a name="lasframeprocessor-java"></a>

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