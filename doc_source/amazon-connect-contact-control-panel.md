# Provide Access to the Contact Control Panel<a name="amazon-connect-contact-control-panel"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to communicate with contacts\. But before agents can access to the CCP and handle contacts, there are a few things you need to do: 
+ [Add agents](user-management.md) to your instance\. This creates a user name and password for them to log into the CCP\. 
+ [Assign them the "Agent" security profile](assign-security-profile.md)\. This grants them permissions to access the CCP\.
+ Give them their user name, password, and a link to the CCP so they can log in\. The CCP is a website\. The URL to your CCP is:
  + **https://*name of your instance*\.awsapps\.com/connect/ccp\-v2/**

We recommend telling agents to bookmark the URL to the CCP so they can access it easily\.

As the admin, you can access the CCP by clicking on the phone icon in the upper right corner of Amazon Connect\.

For information about using the CCP, see [Using the CCP \(the Agent UI\)](agent-user-guide.md)\. 

## Grant Microphone Access in Chrome, Firefox, or Edge<a name="accessing-microphone"></a>

If agents experience problems with their microphone, they may need to grant microphone access in their browser\. Choose one of the following articles to get the steps appropriate for your browser:
+ [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)
+ [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)
+ [Windows 10 camera, microphone, and privacy](https://support.microsoft.com/en-us/help/4468232/windows-10-camera-microphone-and-privacy): includes instructions for Microsoft Edge

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox as your browser\.

## How to Get Help for CCP Issues<a name="how-to-get-help-for-ccp-issues"></a>

**Agents**: Contact your manager or the technical support provided by your company\. 

**Amazon Connect Administrators**: See [Troubleshooting Issues with the CCP](troubleshooting.md) for detailed troubleshooting steps\. Or, log in to the [AWS Management Console](https://console.aws.amazon.com/console) \(https://console\.aws\.amazon\.com/console\) using your AWS account\. In the upper right corner of the page, choose **Support**, and open a support ticket\.