# Step 1: Handle a Voice Contact<a name="tutorial1-explore-voice"></a>

1. On the navigation menu, choose **Dashboard**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-dashboard-menu.png)

1. On the **Dashboard** page, choose **Test chat**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-test-chat.png)

1. Choose **Activate Contact Control Panel**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-activate-ccp.png)

1. If your browser prompts you to grant microphone access, choose **Allow**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-allow-microphone.png)

1. If your browser prompts you to allow notifications, choose **Allow**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-allow-notifications.png)

1. In the test CCP, set your status to **Available**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-testccp-available.png)

1. Use your mobile phone to call the phone number that you claimed earlier\. If you didn't write down the number, you can find it by going to **Routing**, **Phone numbers**\.

1. When your call is joined to Amazon Connect you'll hear "Press 1 to be put in queue for an agent, 2 to \.\.\." This is the [Sample Inbound Flow](sample-inbound-flow.md) that Amazon Connect runs by default\. You're going to change this later in the tutorial\.

1. You can play around with the different options in the Sample inbound contact flow\. To connect to an agent, press **1**, **1**, **1**\.

1. In the CCP, choose **Accept call**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-accept-call.png)

1. You'll see what the CCP looks like when an agent is connected to a customer\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-first-call.png)

1. Choose **End call**\. 

   Now the contact is in the After Contact Work \(ACW\) state\. This is when the agent might enter some notes about the contact\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-acw.png)

1. Choose **Clear contact**\. This frees up the agent to take another incoming contact\. 

Well done\! You've handled your first voice contact\! 

**Tip**  
As an administrator, you can launch the CCP from anywhere on the Amazon Connect console by choosing the phone icon on the top of the page\.  

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-phone-icon.png)

## Next Step<a name="tutorial1-test-voice-next-step"></a>

Go to [Step 2: Handle a Chat Contact](tutorial1-test-chat.md) to experience how to handle a chat contact\.