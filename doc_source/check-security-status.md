# Contact block: Check security status<a name="check-security-status"></a>

## Description<a name="check-security-status-description"></a>
+ The [Set security behavior](set-security-behavior.md) needs to be set in the contact flow before this one\. It sends audio to [Amazon Connect Voice ID](voice-id.md) to verify the customer's identity, and returns a status\. 
+ The **Check security status** block branches based on one of the following statuses returned by Voice ID:
  + **Authenticated**: The caller's identity has been verified\. That is, the authentication score is greater than or equal to the threshold \(default threshold of 90 or your custom threshold\)\.
  + **Not authenticated**: The authentication score is lower than threshold that you configured\.
  + **Inconclusive**: Unable to analyze a caller's speech for authentication\. This is usually because Voice ID did not get the required 10 seconds to provide a result for verification\. 
  + **Not enrolled**: The caller has not yet been enrolled in voice authentication\. When this status is returned, for example, you may want to directly route the call to an agent for enrollment\.
  + **Opted out**: The caller has opted out of voice authentication\.

## Contact flow types<a name="check-security-status-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer queue flow
+ Customer whisper flow
+ Outbound whisper flow
+ Agent whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="check-security-status-properties"></a>

This block doesn't have any properties that you set\. Rather, it creates branches for you to route contacts based on the result of the authentication threshold and voiceprint evaluation\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-security-status-properties.png)

## Configured block<a name="check-security-status-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-security-status-configured.png)

## More information<a name="check-security-status-more-info"></a>

See the following topic for more information about this block:
+ [Use real\-time caller authentication with Voice ID](voice-id.md)