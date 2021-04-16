# Provide access to the Contact Control Panel<a name="amazon-connect-contact-control-panel"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to communicate with contacts\. But before agents can access to the CCP and handle contacts, there are a few things you need to do: 

1. Create a user name and password for agents to log into the CCP, by [adding agents to your instance](user-management.md)\.

1. [Assign them the **Agent** security profile](assign-security-profile.md)\. This grants them permissions to access the CCP\.

1. Provide the user name, password, and the CCP website link to your agents so they can log in\. 

   The CCP website link is: **https://*instance name*\.awsapps\.com/connect/ccp\-v2/**
**Note**  
IT administrators: In the future, the access URL is going to change\. For the release schedule and technical details, see [Upcoming change: Domain for new Amazon Connect instances is "my\.connect\.aws"New domain for access URL](amazon-connect-release-notes.md#new-domain)\. 

   We recommend telling agents to bookmark the URL to the CCP so they can access it easily\.

1. Train your agents on the CCP:
   + Watch [Training video: How to use the CCPTraining video](ccp-video-training.md)
   + [Download a quick start cheat sheet](https://connectivitytest.s3.amazonaws.com/CCP_Agent_QuickStart_20200615.pptx)\.

## Grant microphone access in Chrome or Firefox<a name="accessing-microphone"></a>

If agents experience problems with their microphone, they may need to grant microphone access in their browser\. Choose one of the following articles to get the steps appropriate for your browser:
+ [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)
+ [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)

Microsoft Edge is not a supported browser for accessing the Contact Control Panel\.

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox as your browser\.

## How to get help for CCP issues<a name="how-to-get-help-for-ccp-issues"></a>

**Agents**: Contact your manager or the technical support provided by your company\. 

**Amazon Connect Administrators**: See [Troubleshooting Issues with the Contact Control Panel \(CCP\)](troubleshooting.md) for detailed troubleshooting steps\. Or, log in to the [AWS Management Console](https://console.aws.amazon.com/console) \(https://console\.aws\.amazon\.com/console\) using your AWS account\. In the upper right corner of the page, choose **Support**, and open a support ticket\.