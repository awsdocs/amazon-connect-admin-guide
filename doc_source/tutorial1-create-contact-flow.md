# Step 4: Create a contact flow<a name="tutorial1-create-contact-flow"></a>

Although Amazon Connect comes with a set of [built\-in contact flows](contact-flow-default.md), you can create your own contact flows to determine how a customer experiences your contact center\. The contact flows contain the prompts that customers hear or see, and they transfer them to the right queue or agent, among other things\.

In this step, create a contact flow that's specific to the IT Help Desk experience that you're creating\.

1. On the navigation menu, go to **Routing**, **Contact flows**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-routing-contact-flows.png)

1. Choose **Create contact flow**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-create-contact-flow.png)

1. The contact flow designer opens\. Enter a name for the contact flow, such as **Test contact flow**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-name-contact-flow.png)

1. Choose the drop\-down arrows to expand the sections to access the blocks in them\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-expand-contact-flow.png)

1. Drag the following blocks onto the grid: [Set logging behavior](set-logging-behavior.md) \(in the **Set** group\), [Set voice](set-voice.md) \(in the **Set** group\), and [Play prompt](play.md) \(in the **Interact** group\)\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-blocks1.png)

1. Use your mouse to drag an arrow from the **Start** block to the **Set logging behavior** block\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-connect-blocks1.png)

1. Connect the remaining blocks, as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-connect-blocks2.png)

1. Choose the **Play prompt** title to open its properties page\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt-title.png)

1. Configure the **Play prompt** block, as shown in the following image, and then choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt1.png)

1. Add a [Get customer input](get-customer-input.md) block and connect to the **Play prompt** block\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-get-customer-input3.png)

1. Choose the title of the [Get customer input](get-customer-input.md) block to open the properties page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-get-customer-input.png)

1.  Configure the **Get customer input** block, as shown in the following images\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input1.png)  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input2.png)

1. While still in the **Get customer input** block, choose **Add an intent**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input4.png)

1. Enter the names of the intents that you created in the Amazon Lex bot\. They are case sensitive\!  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input3.png)

1. Choose **Save**\.

1. Add a **Play prompt** block \(from the **Interact** group\) and connect it to the **PasswordReset** branch\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt2.png)

1. Choose the **Play prompt** title to open its properties page\. Configure the **Play prompt** block with the message *We’re putting you in a queue to help you with password reset\.* Choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt3.png)

1. Add a second **Play prompt** block and connect it to the **NetworkIssue** branch\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt4.png)

1. Choose the **Play prompt** title to open its properties page\. Configure the **Play prompt** block with the message *We’re putting you in a queue to help you with your network issues\.* Choose **Save**\.

1. Add a [Disconnect / hang up](disconnect-hang-up.md) block \(from the **Terminate/Transfer** group\) to the grid\. Connect the **Default** and **Error** branches to it\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-disconnect1.png)

1. Add a [Set working queue](set-working-queue.md) block \(from the **Set** group\) to the grid\. Connect the **Play prompt**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-set-working-queue1.png)

1. Choose the **Set working queue** title to open its properties page\. Configure the **Set working queue** block by using the drop\-down arrow to choose the **PasswordReset** queue\. Choose **Save**  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-set-working-queue2.png)

1. Add a **Set working queue** block for NetworkIssue, and configure it with the NetworkIssue queue\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-set-working-queue3.png)

1. Drag two **Transfer to queue** blocks \(from the **Terminate/Transfer** group\) onto the grid\.

1. Connect each of the **Set working queue** blocks to a **Transfer to queue** block, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-transfer-to-queue.png)

1. Drag another **Disconnect/hang up** block onto the grid\. Connect all of the remaining **Error** and **At capacity** branches to it\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-disconnect2.png)

1. The completed contact flow looks similar to the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-contact-flow-finished.png)

1. Choose **Save**, and then choose **Publish**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-save-publish.png)
**Tip**  
Any blocks that aren't connected or configured correctly generate an error\. If this happens, double\-check that all branches are connected\.

1. When the contact flow publishes, it displays the message that it saved successfully\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-contact-flow-published.png)

   If the contact flow doesn't save, double\-check that all the branches are connected to blocks\. That's the most common reason contact flows don't publish\. 