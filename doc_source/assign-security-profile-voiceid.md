# Security profile permissions for Voice ID<a name="assign-security-profile-voiceid"></a>

Assign the following **VoiceID** permission to the agent's security profile:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-security-profile-permissions.png)
+ **Voice ID \- Access**: Enables controls in the Contact Control Panel so agents can:
  + View authentication outcomes\.
  + Opt\-out or re\-authenticate a caller\.
  + Update `SpeakerID`\.
  + View fraud detection results, rerun fraud analysis \(fraud detection decision, fraud type and score\)\.

The following image shows an example of these controls on the CCP:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-controls.png)

For instructions, see [Update security profiles](update-security-profiles.md)\.

By default, the **Admin** security profile already has permissions to perform all Voice ID activities\.