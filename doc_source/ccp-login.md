# Log in and log out of the Amazon Connect CCP<a name="ccp-login"></a>

Before you can log in to the Contact Control Panel \(CCP\), your administrator must give you the following information: 
+ The URL to launch the CCP:
  + https://*instance name*\.my\.connect\.aws/ccp\-v2/

  Where *instance name* is provided by your IT department or whoever set up Amazon Connect for your business\.
+ Your agent ID\.
+ Your agent password\.

**To log in**

After you have that information, here's how to log in and get started\.

1. Ensure that your USB headset is securely connected to your computer\.

1. Using Chrome or Firefox, open the CCP by using the URL that you received from your administrator\.

1. Enter your agent ID and password, and then choose **Sign In**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-login.png)

1. If you are prompted to allow access to your microphone and speaker, choose **Allow**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-allow-microphone.png)

You're all set to go\!

## Problems logging in?<a name="problems-logging-in-CCP"></a>

If you have problems logging in to the CCP, contact your manager for help, or the IT Department for your organization\.

## Log out of the Amazon Connect CCP<a name="ccp-logout"></a>

**Important**  
Closing the CCP doesn't automatically sign out an agent\. Amazon Connect still tries to route contacts to them\. To change this behavior, a developer can customize CCP for your contact center\. For instructions, see [CCPv1: Log out agents automatically when they close their CCP](automatic-logout.md)\. 

1. At the top of the CCP, choose **Settings**\. 

1. Choose **Log out**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-logout.png)