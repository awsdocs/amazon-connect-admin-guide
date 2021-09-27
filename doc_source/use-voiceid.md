# Use Voice ID<a name="use-voiceid"></a>

This topic shows how Voice ID features appear in your Contact Control Panel \(CCP\)\.

## Enroll a caller in Voice ID<a name="use-voiceid-notenrolled"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-enrollment.png)

1. You receive an incoming call\.

1. The caller is not yet enrolled in Voice ID so you choose **Enroll**\.

1. A message is displayed that Voice ID is sampling the caller's voice\. It requires 30 seconds of speech \(excluding silence\)\. 

1. The caller is now enrolled in Voice ID\. This example also shows the caller's **Fraud risk** as lower than the threshold\.

## Verification of an enrolled caller<a name="use-voiceid-reenroll"></a>

After a customer is enrolled in Voice ID, when they call your contact center again, you can verify they are who they say they are\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-reenroll.png)

1. You receive an incoming call\.

1. The caller is already enrolled in Voice ID, and their status is **Authenticated**\. You can choose to re\-evaluate authentication using Voice ID\.

1. A message is displayed that Voice ID is evaluating the caller's speech\. It requires 10 seconds of speech \(excluding silence\)\. 

1. The caller has been authenticated by Voice ID\. This example also shows the caller's **Fraud risk** is lower than the threshold\.

## Caller has opted out<a name="use-voiceid-optout"></a>

The following image shows what appears in your CCP when a caller has opted out of Voice ID\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-optout.png)

1. You receive an incoming call\.

1. The caller has previously opted out of Voice ID\. 

1. You have the option to enroll them\.

## Authentication status = Not authenticated<a name="use-voiceid-mismatch"></a>

When an enrolled caller calls your contact center, Voice ID may return a result of **Not authenticated**\. This means Voice ID was unable to authenticate a caller's speech\. The authentication score for the caller is lower than the configured threshold\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-not-authenticated.png)

The previous images show that the **Fraud risk** can be **High** or **Low**, independent of whether the caller is authenticated\. 

## Authentication status: Inconclusive<a name="use-voiceid-inconclusive"></a>

When an enrolled customer calls your contact center, Voice ID may return a result of **Inconclusive**: Voice ID was unable to analyze a caller's speech for authentication\. This is usually because Voice ID did not get the required 10 seconds to provide a result for verification\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-inconclusive.png)