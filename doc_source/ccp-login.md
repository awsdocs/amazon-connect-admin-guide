# Log In and Log Out of the Amazon Connect CCP<a name="ccp-login"></a>

Before you can log in to the Contact Control Panel \(CCP\), your administrator must give you the following information: 
+ A link to the CCP\. It looks something like this: https://*name of your center*\.awsapps\.com/connect/ccp\-v2/\.
+ Your agent ID\.
+ Your agent password\.

After you have that information, here's how to log in and get started\.

1. Ensure that your USB headset is securely connected to your computer\.

1. Using Chrome or Firefox, open the CCP by using the URL that you received from your administrator\.

1. Enter your agent ID and password, and then choose **Sign In**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-login.png)

1. If you are prompted to allow access to your microphone and speaker, choose **Allow**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-allow-microphone.png)

You're all set to go\!

## Log Out of the Amazon Connect CCP<a name="w54aac51c21c11"></a>

**Important**  
Closing the CCP window doesn't automatically sign out an agent\. Amazon Connect still tries to route contacts to them\. To change this behavior, a developer can customize CCP for your contact center\. For instructions, see [Log Out Agents Automatically When They Close Their CCP](automatic-logout.md)\. 

1. At the top of the CCP, select the **Change Status** dropdown menu\. 

1. Choose **Log out**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-logout.png)