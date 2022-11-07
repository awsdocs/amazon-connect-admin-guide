# Step 3: Set up routing<a name="tutorial1-set-up-routing"></a>

In this step, you start at the Amazon Connect console for your instance\. This step shows how to set up your queues, create a routing profile, and then assign your user account to the profile\. 

1. On the navigation menu, go to **Routing**, **Queues**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-routing-queues.png)

1. Choose **Add queue**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-new-queue-button.png)

1. Complete the page, as shown in the following image, to add a queue named **PasswordReset**\. When done, choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-create-queue.png)  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-create-queue1.png)

   For the purposes of this tutorial, leave the following empty: Outbound whisper flow, Quick connect, and Maximum contact in queue\. 

1. Add a queue named **NetworkIssue**\. Complete the **Add queue** page like you did for the **PasswordReset** queue\.

   When done, you'll have three queues\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-queues.png)

1. On the navigation menu, go to **Users**, **Routing Profiles**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-routing-profiles.png)

1. Choose **Add routing profile**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-new-profile.png)

1. Assign a name to the new profile \(for example, **Test routing profile**\)\. Enter a description, select **Voice**, **Chat**, and set **Maximum chats** to **1\.**  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-profiles1.png)

1. In the **Queues** section, use the drop\-down arrow to search for the queues you just created\. Choose **NetworkIssue**, select **Voice** and **Chat**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-queue-button.png)

1. Choose **Add Queue**, and then add the **PasswordReset** queue\. Select **Voice** and **Chat**, and then choose **Save**\.

1. Under **Default outbound queue**, use the drop\-down arrow to choose **BasicQueue**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-outbound-queue.png)

1. When done, scroll to the top of the page, and choose **Save** to save the profile\.

1. On the navigation menu, go to **Users**, **User management**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-user-management.png)

1. Select your login name\.

1. In **Settings**, **Routing profile** choose the routing profile you created, for example, **Test routing profile**\. Choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-edit-user2.png)

Routing is all set up and ready to go\. 