# Contact block: Set security behavior<a name="set-security-behavior"></a>

## Description<a name="set-security-behavior-description"></a>
+ Sets options for authenticating callers using Amazon Connect Voice ID\. For more information about this feature, see [Use real\-time caller authentication with Voice ID](voice-id.md)\.
+ Sends audio to Amazon Connect Voice ID to verify the caller's identity, as soon as the call is connected to a contact flow\.
+ Use a [Check security status](check-security-status.md) block after this one to branch based on the results of the verification\.

## Supported channels<a name="set-security-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Contact flow types<a name="set-security-behavior-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Customer whisper flow
+ Outbound whisper flow
+ Agent whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-security-behavior-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-security-behavior-properties.png)
+ **Voice authentication**: Set to **On** to begin streaming the customer channel of the audio to Voice ID\.
+ **Authentication threshold**: When Voice ID compares the voiceprint of the caller to the enrolled voiceprint of the claimed identity, it generates an authentication score between 0\-100\. This score indicates the confidence of a match\. You can configure a threshold for the score which indicates whether the caller is authenticated\. The default threshold of 90 provides high security for most cases\. 
  + If the authentication score is below the configured threshold, Voice ID treats the call as not authenticated\.
  + If the authentication score is above the configured threshold, Voice ID treats the call as authenticated\.

  For example, if the person is sick and calling from a mobile device in their car, the authentication score is going to be slightly lower than when the person is well and calling from a quiet room\. If an imposter is calling, the authentication score is much lower\.

## Configuration tips<a name="set-security-behavior-tips"></a>
+ For the **Authentication threshold**, we recommend that you start with the default of 90 and adjust until you find a good balance for your business\.

  Every time you increase the value of the **Authentication threshold** beyond the default of 90, there's a tradeoff: 
  + The higher the threshold, the greater the false reject rate \(FRR\), that is, the likelihood that an agent will need to verify the customer's identity\.

    For example, if you set it too high, such as greater than 95, agents will need to verify every customer's identity\.
  + The lower the threshold, the greater the false reject rate \(FRR\), that is, the likelihood that Voice ID will incorrectly accept an access attempt by an unauthorized caller\.
+ When Voice ID verifies that the voice belongs to the enrolled customer, it returns a status of **Authenticated**\. Add a [Check security status](check-security-status.md) to branch based on the returned status\.

## Configured block<a name="set-security-behavior-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-security-behavior-configured.png)

## More information<a name="set-security-behavior-more-info"></a>

See the following topic for more information about this block:
+ [Use real\-time caller authentication with Voice ID](voice-id.md)