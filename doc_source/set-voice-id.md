# Contact block: Set Voice ID<a name="set-voice-id"></a>

## Description<a name="set-voice-id-description"></a>
+ Enables audio streaming and sets thresholds for voice authentication and detection of fraudsters in a watchlist\. For more information about this feature, see [Use real\-time caller authentication with Voice ID](voice-id.md)\.
+ Sends audio to Amazon Connect Voice ID to verify the caller's identity and match against fraudsters in watchlist, as soon as the call is connected to a contact flow\.
+ Use a [Check Voice ID](check-voice-id.md) block after this one to set the customer ID for the caller\.
+ Use a [Check Voice ID](check-voice-id.md) block after this one to branch based on the results of the enrollment check, authentication, or fraud detection\. 
+ For information about how to use this block in a contact flow, along with [Check Voice ID](check-voice-id.md) and [Set contact attributes](set-contact-attributes.md), see [Step 2: Configure Voice ID in your contact flow](enable-voiceid.md#enable-voiceid-step2) in [Enable Voice ID](enable-voiceid.md)\. 

## Supported channels<a name="set-security-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Contact flow types<a name="set-voice-id-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Customer whisper flow
+ Outbound whisper flow
+ Agent whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-voice-id-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-id-properties.png)

### Start streaming audio for Voice ID<a name="set-voice-id-properties-streaming-audio"></a>

When this option is selected, Amazon Connect begins streaming audio from the customer's channel to Voice ID\.

You can add this block several places in a contact flow, but after **Start streaming audio** is selected, it cannot be disabled, even if later in the flow there are other **Set Voice ID** blocks that do not have it enabled\.

### Voice authentication<a name="set-voice-id-properties-voice-authentication"></a>

**Authentication threshold**: When Voice ID compares the voiceprint of the caller to the enrolled voiceprint of the claimed identity, it generates an authentication score between 0\-100\. This score indicates the confidence of a match\. You can configure a threshold for the score which indicates whether the caller is authenticated\. The default threshold of 90 provides high security for most cases\. 
+ If the authentication score is below the configured threshold, Voice ID treats the call as not authenticated\.
+ If the authentication score is above the configured threshold, Voice ID treats the call as authenticated\.

For example, if the person is sick and calling from a mobile device in their car, the authentication score is going to be slightly lower than when the person is well and calling from a quiet room\. If an imposter is calling, the authentication score is much lower\.

### Authentication response time<a name="set-voice-id-properties-authentication-response-time"></a>

You can set the authentication response time between 5 and 10 seconds, which determines how quickly you want Voice ID authentication analysis to complete\. Lowering it makes the response time faster at the tradeoff of lower accuracy\. When you're using self\-service IVR options where callers do not talk a lot, you may want to reduce this time\. You can then increase the time if the call needs to be transferred to an agent\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-id-properties2.png)

Use attributes to set the authentication threshold dynamically\. For example, you may want to raise the threshold based on the membership level of the customer, or the type of transaction or information they are calling about\.

### Fraud detection<a name="set-voice-id-properties-fraud-detection"></a>

The threshold you set for fraud detection is used to measure risk\. Scores higher than the threshold are reported as higher risk\. Scores lower than the threshold are reported as lower risk\. Raising the threshold lowers false positive rates \(makes result more certain\), but raises false negative rates 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-id-properties3.png)

Use attributes to set the fraud threshold dynamically\. For example, you may want to lower the threshold for high wealth customers, or the type of transaction or information they are calling about\.

## Configuration tips<a name="set-voice-id-tips"></a>
+ For the **Authentication threshold**, we recommend that you start with the default of 90 and adjust until you find a good balance for your business\.

  Every time you increase the value of the **Authentication threshold** beyond the default of 90, there's a tradeoff: 
  + The higher the threshold, the greater the false reject rate \(FRR\), that is, the likelihood that an agent will need to verify the customer's identity\.

    For example, if you set it too high, such as greater than 95, agents will need to verify every customer's identity\.
  + The lower the threshold, the greater the false acceptance rate \(FAR\), that is, the likelihood that Voice ID will incorrectly accept an access attempt by an unauthorized caller\.
+ When Voice ID verifies that the voice belongs to the enrolled customer, it returns a status of **Authenticated**\. Add a [Check Voice ID](check-voice-id.md) block to you flow branch based on the returned status\.
+ For the **Fraud threshold**, we recommend that you start with the default of 20 and adjust until you find a good balance for your business\.

  If the caller's score is above the threshold, it indicates there's a higher risk for fraud in that call\.

## Configured block<a name="set-voice-id-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-id-configured.png)

## More information<a name="set-voice-id-more-info"></a>

See the following topic for more information about this block:
+ [Use real\-time caller authentication with Voice ID](voice-id.md)
+ [Contact block: Check Voice ID](check-voice-id.md)
+ [Use Voice ID](use-voiceid.md)