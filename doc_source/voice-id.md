# Use real\-time caller authentication with Voice ID<a name="voice-id"></a>

Amazon Connect Voice ID provides real\-time caller authentication and fraud risk detection which make voice interactions in contact centers more secure and efficient\. Voice ID uses machine learning to verify the identity of genuine customers by analyzing a caller's unique voice characteristics\. This allows contact centers to use an additional security layer that doesn't rely on the caller answering multiple security questions, and makes it easy to enroll and verify customers without changing the natural flow of their conversation\. Voice ID also offers real\-time detection of fraudsters who frequently target your contact center, thereby reducing losses due to fraud\.

With Amazon Connect Voice ID you can:
+ Passively enroll customers for voice authentication without requiring them to repeat a particular word or phrase\.
+ Migrate customers into Voice ID by enrolling them in batch\.
+ Verify the enrolled customer's identity by analyzing their unique voice characteristics\.
+ Detect fraudsters from a watchlist that you have created\.
+ Detect voice spoofing\.

## How Voice ID works<a name="how-voice-id-works"></a>

### Customer enrollment<a name="customer-enrollment"></a>

1. When a customer calls for the first time, the agent confirms the identity of the caller by using existing security measures, such as asking for mother's maiden name or a one\-time passcode \(OTP\) delivered by SMS\. This ensures that only genuine customers are enrolled in Voice ID\. 

1. Voice ID starts listening to the customer's speech after the contact has encountered the [Set Voice ID](set-voice-id.md) block, where Voice ID is enabled\. Voice ID listens to the call until one of the following happens: 
   + It gets enough audio to evaluate the speaker for authentication, fraud, and enroll the speaker \(if requested\)\. This is 30 seconds of customer speech, excluding silence\.
   + The call ends\.

1. Voice ID then creates the enrollment voiceprint\. A voiceprint is a mathematical representation that implicitly captures unique aspects of an individual's voice such as speech rhythm, pitch, intonation, and loudness\. 

   The caller does not need to say or repeat any specific phrases to enroll in Voice ID\.

### Customer authentication<a name="customer-verification"></a>

1. When the enrolled customer calls back in, they are verified through an interaction with an IVR, or during their interaction with an agent\. 

   By default Voice ID is configured to require 10 seconds of a caller's speech to authenticate, which can be done as part of a typical customer interaction in the IVR or with the agent \(such as "what's your first and last name?" and "what are you calling about?"\)\. You can adjust the amount of required speech using the [Authentication response time](set-voice-id.md#set-voice-id-properties-authentication-response-time) property in the [Set Voice ID](set-voice-id.md) block\.

1. Voice ID uses the audio to generate the caller's voiceprint and compares it with the enrolled voiceprint corresponding to the claimed identity, and returns an authentication result\. 

For more information about the agent's experience, see [Use Voice ID](use-voiceid.md)\.

## How much speech is needed for enrollment and authentication<a name="how-long-for-enrollment"></a>
+ Enrollment: 30 seconds of customer net speech \(speech that excludes any silence\) to create a voiceprint and enroll a customer\.
+ Verification: By default, 10 seconds of customer net speech to verify that the voice belongs to the claimed identity\. The speech can be from interacting with an IVR or an agent\. You can adjust the amount of required speech using the [Authentication response time](set-voice-id.md#set-voice-id-properties-authentication-response-time) property in the [Set Voice ID](set-voice-id.md)\.

## Batch enrollment<a name="batch-enrollment"></a>

You can get a jump start on using biometrics by batch enrolling customers who have already consented for biometrics\. Using stored audio recordings in your S3 bucket, and a JSON input file that provides the speaker identifier and a link to the audio recordings, you can invoke the Voice ID batch APIs\. 

For more information, see [Batch enrollment using audio data from prior calls](voiceid-batch-enrollment.md)\.

## Known fraudster detection<a name="fraud-detection"></a>

1. Create a watchlist of known fraudsters by using fraudster registration API on your stored audio recordings in your S3 bucket\. For more information, see [Create and edit a fraudster watchlist](voiceid-fraudster-watchlist.md)\. 

1. When a fraudster from the watchlist calls in, Voice ID analyzes the call audio to return a risk score and outcome to indicate how closely the caller's voiceprint matches the fraudsters voiceprint that is created from audio recordings from your S3 bucket\.

## Voice spoofing detection<a name="voice-spoofing-detection"></a>

1. When a prospective fraudster tries to spoof caller audio using audio playback or synthesized speech, Voice ID returns a risk score and outcome to indicate the how likely it is that the voice is spoofed\.

1. By enabling fraud detection in contact flows, you also enable checks for known fraudster risks and voice spoofing risks\. 

## What data is stored?<a name="voice-id-data-storage"></a>

Voice ID stores audio files of the speaker's voice, voiceprints, and speaker identifiers\. This data is encrypted using a KMS key that you provide\.

If you enable detection of fraudsters in a watchlist, Voice ID also stores the fraudster audio and voiceprints\. For more information, see [Data handled by Amazon Connect](data-handled-by-connect.md)\.

### Expired speakers<a name="voice-id-expired-speakers"></a>

For BIPA compliance, Voice ID automatically expires speakers that have not been accessed for enrollment, re\-enrollment, or successful authentication for three years\.

To view a speaker’s last access, look at the `lastAccessedAt` attribute that is returned by the `DescribeSpeaker` and `ListSpeakers` APIs\. 

If you try to use the `EvaluateSesssion` API to authenticate an expired speaker, a `SPEAKER_EXPIRED` authentication decision is returned\. 

To use the expired speaker again, they must be re\-enrolled\.