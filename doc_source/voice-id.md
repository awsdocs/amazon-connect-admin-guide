# Use real\-time caller authentication with Voice ID<a name="voice-id"></a>


|  | 
| --- |
| The Voice ID feature is in preview release for Amazon Connect and is subject to change\. | 

Amazon Connect Voice ID provides real\-time caller authentication which makes voice interactions in contact centers more secure and efficient\. Voice ID uses machine learning to verify the identity of genuine customers by analyzing a caller’s unique voice characteristics\. This allows contact centers to use an additional security layer that doesn’t rely on the caller answering multiple security questions, and makes it easy to enroll and verify customers without changing the natural flow of their conversation\. 

With Amazon Connect Voice ID you can:
+ Passively enroll customers for voice authentication without requiring them to repeat a particular word or phrase\.
+ Verify the enrolled customer's identity by analyzing their unique voice characteristics\.

## How Voice ID works<a name="how-voice-id-works"></a>

There are two steps related to voice authentication: customer enrollment and customer verification\. 

### Customer enrollment<a name="customer-enrollment"></a>

1. When a customer calls for the first time, the agent confirms the identity of the caller by using existing security measures, such as asking for mother’s maiden name or a one\-time passcode \(OTP\) delivered by SMS\. This ensures that only genuine customers are enrolled in Voice ID\. 

1. After the agent makes the enrollment request, Voice ID listens to the call until it has captured 30 seconds of customer speech \(excluding silence\)\. 

1. Voice ID then creates the enrollment voiceprint\. A voiceprint is a mathematical representation that implicitly captures unique aspects of an individual’s voice such as speech rhythm, pitch, intonation, and loudness\. 

   The caller does not need to say or repeat any specific phrases to enroll in Voice ID\.

### Customer verification<a name="customer-verification"></a>

1. When the enrolled customer calls back in, they are verified through an interaction with an IVR, or during their interaction with an agent\. 

   Voice ID needs 10 seconds of a caller’s speech to authenticate, which can be done as part of a typical customer interaction in the IVR or with the agent \(such as "what’s your first and last name?" and "what are you calling about?"\)\.

1. Voice ID uses the audio to generate the caller’s voiceprint and compares it with the enrolled voiceprint corresponding to the claimed identity, and returns an authentication result\.  

## Enable Voice ID<a name="setup-voice-id"></a>

To enable Voice ID, add the following blocks to your contact flow: 
+ [Set security behavior](set-security-behavior.md): Add this block to the start of a call\. You use this block to send audio to Amazon Connect Voice ID to verify the caller's identity, as soon as the call is connected to a contact flow\. Set the following properties:
  + **Voice authentication**: Set to **On** to begin streaming the customer channel of the audio to Voice ID\.
  + **Authentication threshold**: When Voice ID compares the voiceprint of the caller to the enrolled voiceprint of the claimed identity, it generates an authentication score between 0\-100\. This score indicates the confidence of a match\. You can configure a threshold for the score which indicates whether the caller is authenticated\. The default threshold of 90 provides high security for most cases\. 
    + If the authentication score is below the configured threshold, Voice ID treats the call as not authenticated\.
    + If the authentication score is above the configured threshold, Voice ID treats the call as authenticated\.

    For example, if the person is sick and calling from a mobile device in their car, the authentication score is going to be slightly lower than when the person is well and calling from a quiet room\. If an imposter is calling, the authentication score is much lower\.
+ [Set contact attributes](set-contact-attributes.md): Use to pass the customer ID to Voice ID\. The customer ID may be an customer number from your CRM, for example\.
+ [Check security status](check-security-status.md): Use to check the response from Voice ID, and then branch based on one of the following statuses:
  + **Authenticated**: The caller's identity has been verified\. That is, the authentication score is greater than or equal to the threshold \(default threshold of 90 or your custom threshold\)\.
  + **Not authenticated**: The authentication score is lower than threshold that you configured\.
  + **Inconclusive**: Unable to analyze a caller's speech for authentication\. This is usually because Voice ID did not get the required 10 seconds of speech to provide a result for verification\. 
  + **Not enrolled**: The caller has not been enrolled in voice authentication\. When this status is returned, for example, you may want to directly route the call to an agent for enrollment\.
  + **Opted out**: The caller has opted out of voice authentication\.

## Sample Voice ID contact flow<a name="sample-voice-id-flow"></a>

1. When a customer calls for the first time, their customer ID is passed to Voice ID using the [Set contact attributes](set-contact-attributes.md) block\.

1. Voice ID looks for the customer ID in its database\. Since it's not there, Voice ID starts listening to the audio to create a voiceprint\.

   

1. When the voiceprint is complete, it sends a **Not enrolled** result message\. The [Check security status](check-security-status.md) block branches based on this result, and you can decide what the next step should be\. For example, you might want to customize your agent application to add **Enroll** button so agents can enroll the customer in voice authentication\. 

1. The next time the customer calls, Voice ID finds their customer ID in the database\. It compares the caller’s voiceprint and other representations with similar historical representations associated with the claimed identity\. It returns a result based on the **Authentication threshold** property you configured in the [Set security behavior](set-security-behavior.md) block\.

1. After it evaluates the speech, and returns the message **Authenticated** if the voiceprints are similar\. Or it returns one of the other statuses\.

1. The contact is then routed down the appropriate branch by the [Check security status](check-security-status.md) block\.

## How much speech is needed for enrollment and verification<a name="how-long-for-enrollment"></a>
+ Enrollment: 30 seconds of customer net speech \(speech that excludes any silence\) to create a voiceprint and enroll a customer\.
+ Verification: 10 seconds of customer net speech to verify that the voice belongs to the claimed identity\. The speech can be from interacting with an Amazon Lex bot or an agent\.

## Amazon Connect Streams Voice ID APIs<a name="voice-id-apis"></a>

Use the following [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) APIs to integrate Voice ID into your existing agent web applications\. 
+ `enrollSpeakerInVoiceId`: Enroll a customer to Voice ID using a click of a button\.
+ `evaluateSpeakerWithVoiceId`: Check the customer's Voice ID verification status\. 
+ `optOutVoiceIdSpeaker`: Opt out a customer from Voice ID\.
+ `getVoiceIdSpeakerStatus`: Describe the enrollment status of a customer\.
+ `getVoiceIdSpeakerId`: Get the speaker ID\.
+ `updateVoiceIdSpeakerId`: Update the speaker ID\.

## What data is stored?<a name="voice-id-data-storage"></a>

Voice ID stores voiceprints and customer IDs\. The data is encrypted\.