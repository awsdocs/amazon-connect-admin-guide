# Security profile permissions for Voice ID<a name="assign-security-profile-voiceid"></a>
+ To enable users to search for contacts by their Voice ID status, assign the following **Analytics and Optimization** permission to their security profile:
  + **Voice ID \- attributes and search**: Enables users to search for and view Voice ID results on the **Contact detail** page\. 
+ To grant agents access to Voice ID in the Contact Control Panel, assign the following permission in the **Contact Control Panel** group:
  + **Voice ID \- Access**: Enables controls in the Contact Control Panel so agents can:
    + View authentication outcomes\.
    + Opt\-out or re\-authenticate a caller\.
    + Update `SpeakerID`\.
    + View fraud detection results, rerun fraud analysis \(fraud detection decision, fraud type and score\)\.

The following image shows an example of these controls on the CCP:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ccp-controls.png)

For information about how add more permissions to an existing security profile, see [Update security profiles](update-security-profiles.md)\.

By default, the **Admin** security profile already has permissions to perform all Voice ID activities\.