# Flow block: Check Voice ID<a name="check-voice-id"></a>

## Description<a name="check-voice-id-description"></a>

**Note**  
The [Set Voice ID](set-voice-id.md) block needs to be set in the flow before this one\. That block sends audio to [Amazon Connect Voice ID](voice-id.md) to verify the customer's identity, and returns a status\. 

The **Check Voice ID** block branches based on the results of the voice analysis and the status returned by Voice ID:
+ **Enrollment status**: 
  + **Enrolled**: The caller is enrolled in voice authentication\.
  + **Not enrolled**: The caller has not yet been enrolled in voice authentication\. When this status is returned, for example, you may want to directly route the call to an agent for enrollment\.
  + **Opted out**: The caller has opted out of voice authentication\.

  You are not charged for checking enrollment status\. 
+ **Voice authentication status**:
  + **Authenticated**: The caller's identity has been verified\. That is, the authentication score is greater than or equal to the threshold \(default threshold of 90 or your custom threshold\)\.
  + **Not authenticated**: The authentication score is lower than threshold that you configured\.
  + **Inconclusive**: Unable to analyze a caller's speech for authentication\. This is usually because Voice ID did not get the required 10 seconds to provide a result for authentication\. 
  + **Not enrolled**: The caller has not yet been enrolled in voice authentication\. When this status is returned, for example, you may want to directly route the call to an agent for enrollment\.
  + **Opted out**: The caller has opted out of voice authentication\.

  You are not charged if the result is **Inconclusive**, **Not enrolled** or **Opted out**\.
+ **Fraud detection status**: 
  + **High risk**: The risk score meets or exceeds the set threshold\.
  + **Low risk**: The risk score did not meet the set threshold\.
  + **Inconclusive**: Unable to analyze a caller's voice for detection of fraudsters in a watchlist\.

  You are not charged if the result is **Inconclusive**\.

**Note**  
For **Enrollment status** and **Voice authentication**, the [Customer ID](connect-attrib-list.md) system attribute needs to be set in [Set contact attributes](set-contact-attributes.md) block because they are acting on a specific customer\. You don't need to do this for **Fraud detection** because it's not acting on a specific customer but rather detecting whether the incoming caller matches a fraudster on your watchlist\. This means it's possible for a customer to be successfully authenticated and still have high fraud risk\. 

## Supported channels<a name="check-voice-id-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Error branch | 
| Task | No \- Error branch | 

## Flow types<a name="check-voice-id-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer queue flow
+ Customer whisper flow
+ Outbound whisper flow
+ Agent whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="check-voice-id-properties"></a>

This block doesn't have any properties that you set\. Rather, it creates branches for you to route contacts based on the result of the authentication threshold and voiceprint evaluation that [Set Voice ID](set-voice-id.md) returns\.

The following image shows what this block looks like when it's configured to check for Enrollment status\. Different status results are returned when it's configured for **Voice authentication** or **Fraud detection**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-voice-id-properties.png)

## Configuration tips<a name="check-voice-id-tips"></a>

When you create a flow that uses this block, add these blocks in the following order:

1. [Set Voice ID](set-voice-id.md) block\. 

1. [Set contact attributes](set-contact-attributes.md) block: For **Enrollment status** and **Voice authentication**, the [Customer ID](connect-attrib-list.md) system attribute needs to be set in [Set contact attributes](set-contact-attributes.md) block because it is acting on a specific customer\.

1. **Check Voice ID** block\.

## Configured block<a name="check-voice-id-configured"></a>

The following image shows what this block looks like when it's configured to check for: 

1. Enrollment status

1. Voice authentication

1. Fraud detection

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-voice-id-configured.png)

## More information<a name="check-voice-id-more-info"></a>

See the following topic for more information about this block:
+ [Use real\-time caller authentication with Voice ID](voice-id.md)
+ [Use Voice ID](use-voiceid.md)