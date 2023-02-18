# Provide access to the Contact Control Panel<a name="amazon-connect-contact-control-panel"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to communicate with contacts\. But before agents can access to the CCP and handle contacts, there are a few things you need to do: 

1. Create a user name and password for agents to log into the CCP, by [adding agents to your instance](user-management.md)\.

1. At minimum, [assign them the **Agent** security profile](assign-security-profile.md)\. This grants them permissions to access the CCP, which they use to manage contacts\. 

1. Provide the user name, password, and the CCP website link to your agents so they can log in\. 

   The CCP website link is: **https://*instance name*\.my\.connect\.aws/ccp\-v2/**

   We recommend telling agents to bookmark the URL to the CCP so they can readily access it\.

1. Train your agents on the CCP:
   + Watch [Training video: How to use the CCP](ccp-video-training.md)

## Agent application: Everything in one place<a name="use-agent-application"></a>

Want your agents to manage contacts, and access customer profiles, cases, and knowledge all in one place? Use the [agent application](agent-user-guide.md)\! 

The [agent application](agent-user-guide.md) is a single web browser interface that hosts the CCP, [Customer Profiles](use-customer-profiles.md), [Cases](use-cases.md), and [Wisdom](use-wisdom.md)\.

If you're using the CCP that is provided with Amazon Connect, after you enable Customer Profiles, Cases, or Wisdom, share the following URL with your agents so they can access it:
+ **https://*instance name*\.my\.connect\.aws/agent\-app\-v2/**

If you access your instance using the **awsapps\.com** domain, use the following URL: 
+ **https://*instance name*\.awsapps\.com/connect/agent\-app\-v2/**

For help finding your instance name, see [Find your Amazon Connect instance name](find-instance-name.md)\.

## Grant microphone access in Chrome, Firefox, or Edge<a name="accessing-microphone"></a>

If agents experience problems with their microphone, they may need to grant microphone access in their browser\. Choose one of the following articles to get the steps appropriate for your browser:
+ [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)
+ [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)
+ *How to allow a website to use your camera or microphone while browsing in Microsoft Edge* in the article [Windows camera, microphone, and privacy](https://support.microsoft.com/en-us/windows/windows-camera-microphone-and-privacy-a83257bc-e990-d54a-d212-b5e41beba857)

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox or Edge as your browser\.

## How to get help for CCP issues<a name="how-to-get-help-for-ccp-issues"></a>

**Agents**: Contact your manager or the technical support provided by your company\. 

**Amazon Connect Administrators**: See [Troubleshooting Issues with the Contact Control Panel \(CCP\)](troubleshooting.md) for detailed troubleshooting steps\. Or, log in to the [AWS Management Console](https://console.aws.amazon.com/console) \(https://console\.aws\.amazon\.com/console\) using your AWS account\. In the upper right corner of the page, choose **Support**, and open a support ticket\.