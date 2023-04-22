# Step 3: Set up routing<a name="tutorial1-set-up-routing"></a>

In this step, you start at the Amazon Connect console for your instance\. This step shows how to set up your queues, create a routing profile, and then assign your user account to the profile\. 

1. On the navigation menu, go to **Routing**, **Queues**\.   
![\[The Amazon Connect navigation menu, the Routing icon, the Queues option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-routing-queues.png)

1. Choose **Add queue**\.  
![\[The Queues page, the Add queue button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-new-queue-button.png)

1. Complete the **Add queue** page, as shown in the following image, to add a queue named **PasswordReset**\. When done, choose **Save**\.  
![\[The Add queue page, Queue details section and Hours of operation section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-create-queue.png)

   The following image shows the **Settings** section of the **Add queue** page\. Add your default caller ID name and outbound caller ID number\.  
![\[The Add queue page, settings section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-create-queue1.png)

   For the purposes of this tutorial, leave the following empty: Outbound whisper flow, Quick connect, and Maximum contact in queue\. 

1. Add a queue named **NetworkIssue**\. Complete the **Add queue** page like you did for the **PasswordReset** queue\.

   When done, you'll have three queues\.  
![\[The Queues page, the Basic queue, the Network Issue queue, and the Password Reset queue.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-queues.png)

1. On the navigation menu, go to **Users**, **Routing Profiles**\.   
![\[The Amazon Connect navigation menu, the Users icon, the Routing profiles option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-routing-profiles.png)

1. Choose **Add routing profile**\.   
![\[The Routing profiles page, the Add routing profile button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-new-profile.png)

1. Assign a name to the new profile \(for example, **Test routing profile**\)\. Enter a description, select **Voice**, **Chat**, and set **Maximum chats** to **1\.**  
![\[The Routing profile details section, and settings section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-profiles1.png)

1. In the **Queues** section, use the drop\-down arrow to search for the queues you just created\. Choose **NetworkIssue**, select **Voice** and **Chat**\. Choose **Add Queue**\.  
![\[The Queues section, the Add queue button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-queue-button.png)

1. Add the **PasswordReset** queue\. Select **Voice** and **Chat**, and then choose **Save**\.

1. Under **Default outbound queue**, use the drop\-down arrow to choose **BasicQueue**\.  
![\[The Default outbound queue section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-outbound-queue.png)

1. When done, scroll to the top of the page, and choose **Save** to save the profile\.

1. On the navigation menu, go to **Users**, **User management**\.   
![\[The Amazon Connect navigation menu, Users icon, User management option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-user-management.png)

1. On the **User management** page, select your login name\.

1. On the **Edit** page, in the **Settings** section, in the **Routing profile** dropdown menu, choose the routing profile you created, for example, **Test routing profile**\. Choose **Save**\.  
![\[The settings section, routing profile dropdown menu.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-edit-user2.png)

Routing is all set up and ready to go\. 