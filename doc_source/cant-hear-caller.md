# Can't Hear Caller Or Caller Can't Hear Agent?<a name="cant-hear-caller"></a>

When the agent can't hear the caller or the caller can't hear them, it's usually because there are problems with one of the following: 
+ The connection between the agent's headset and computer\.
+ The permissions for the browser microphone\. 

Here's what you need to check:
+ **Headset connectivity**—Check the settings in Device Manager to ensure that your computer recognizes the headset and allows proper headset connectivity\. For example, if you're using a Windows PC, go to **Device Manager**, then expand **Audio inputs and outputs**\. If your computer recognizes your headset, you'll see it listed there\. 
+ **Browser settings for headset/microphone**—In Chrome, go to **Settings**, **Site Settings**, **Microphone**\. Then check that the correct headset is enabled\. Or, in Firefox, while in the CCP, choose the lock icon in the address bar\. If needed, grant permissions to the CCP\. To learn more, see [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en) or [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)\.

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox as your browser\.

For more information about solving audio problems, see [Troubleshooting Issues with the CCP](troubleshooting.md)\. 