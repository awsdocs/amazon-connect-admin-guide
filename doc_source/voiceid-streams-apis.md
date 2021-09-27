# Amazon Connect Streams Voice ID APIs<a name="voiceid-streams-apis"></a>

Use the following [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) APIs to integrate Voice ID into your existing agent web applications\. 
+ `enrollSpeakerInVoiceId`: Enroll a customer to Voice ID after obtaining their consent to enroll\. 
+ `evaluateSpeakerWithVoiceId`: Check the customer's Voice ID authentication status, and to detect fraudsters\.
+ `optOutVoiceIdSpeaker`: Opt out a customer from Voice ID\.
+ `getVoiceIdSpeakerStatus`: Describe the enrollment status of a customer\.
+ `getVoiceIdSpeakerId`: Get the `SpeakerID` for a customer\.
+ `updateVoiceIdSpeakerId`: Update the `SpeakerID` for a customer\.

You can also use the Voice ID widget in the Contact Control Panel \(CCP\) if you don't want to build a custom agent interface\. For more information about Voice ID in the CCP, see [Use Voice ID](use-voiceid.md)\.