# Can't hear caller or caller can't hear agent?<a name="cant-hear-caller"></a>

When the agent can't hear the caller or the caller can't hear them, it's usually because there are problems with one of the following: 
+ The connection between the agent's headset and computer\.
+ The permissions for the browser microphone\. 

Here's what you need to do:
+ **Check that your computer recognizes your headset**—Check the settings in Device Manager to ensure that your computer recognizes the headset and allows proper headset connectivity\. For example, if you're using a Windows PC:

  1. Go to **Device Manager**, then expand **Audio inputs and outputs**\.

  1. If your computer recognizes your headset, you'll see it listed there\.
+ **Check your browser settings for your headset/microphone**
  + **Chrome**

    1. go to **Settings**, **Site Settings**, **Microphone**\.

    1. Then check that the correct headset is enabled\.

    1.  To learn more, see [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)\.
  + **Firefox**

    1. While in the CCP, choose the lock icon in the address bar\. If needed, grant permissions to the CCP\.

    1.  To learn more, see [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)\.
+ **Remove your ad blocker**: If you're using an ad blocker extension, remove it and see if that fixes the problem\.

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox or Edge as your browser\.

For more information about solving audio problems, see [Troubleshooting Issues with the Contact Control Panel \(CCP\)](troubleshooting.md)\. 