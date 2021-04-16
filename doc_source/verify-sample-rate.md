# Humming sound in headset: Verify the headset and browser sample rates<a name="verify-sample-rate"></a>

If the agent's audio device does not support up to 48khz and the browser asserts a sample rate of 48khz, audio issues such as an audible humming sound may be present in the agent's outgoing audio\. This has been seen with Firefox but not with Chrome\. 

Perform the following steps to verify your headset and browser sample rates\.

## Verify Firefox sample rate<a name="verify-firefox-samplerate"></a>

1. Open the agent's CCP in FireFox, and set their status to **Available**\.

1. Accept a call\.

1. Open a second Firefox tab, and type **about:support **in the Search box\.

1. Scroll down the page to **Media**\.

1. Verify that the sample rates for the input and output devices are **48000**, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/firefox-sample-rate.png)

## Verify Chrome sample rate<a name="verify-chrome-samplerate"></a>

1. Open the agent's CCP in Chrome, and set their status to **Available**\.

1. Accept a call\.

1. Open a second Chrome tab, and type **chrome://about **in the Search box\.

1. Scroll down the page and choose **chrome://media\-internals**\.

1. On the **Audio** tab, choose the **Input Controllers** and verify that the sample rate is **48000**\. Then verify the sample rate for the Output Controllers\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chrome-sample-rate.png)