# Step 4: Create a flow<a name="tutorial1-create-contact-flow"></a>

Although Amazon Connect comes with a set of [built\-in flows](contact-flow-default.md), you can create your own flows to determine how a customer experiences your contact center\. The flows contain the prompts that customers hear or see, and they transfer them to the right queue or agent, among other things\.

In this step, create a flow that's specific to the IT Help Desk experience that you're creating\.

1. On the Amazon Connect navigation menu, go to **Routing**, **Flows**\.  
![\[The navigation menu, Routing icon, Contact flows option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-routing-contact-flows.png)

1. Choose **Create flow**\.  
![\[On contact flows and flow modules page the create contact flow button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-create-contact-flow.png)

1. The flow designer opens\. Enter a name for the flow, such as **Test flow**\.  
![\[The flow designer, the option to edit the name of the flow.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-name-contact-flow.png)

1. Use the search box to search for the following block, and drag them onto the grid: [Set logging behavior](set-logging-behavior.md), [Set voice](set-voice.md), and [Play prompt](play.md)\.   
![\[The flow designer, set logging behavior block, set voice block, play prompt block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-blocks1.png)

1. Use your mouse to drag an arrow from the **Entry** block to the **Set logging behavior** block\.   
![\[The flow designer, set logging behavior block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-connect-blocks1.png)

1. Connect the remaining blocks, as shown in the following image\.   
![\[The flow designer, set logging behavior block, set voice block, play prompt block all connected.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-connect-blocks2.png)

1. Choose the **Play prompt** title to open its properties page\.   
![\[The flow designer, play prompt block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt-title.png)

1. Configure the **Play prompt** block, as shown in the following image, and then choose **Save**\.  
![\[The play prompt block, properties page, text-to-speech or chat text, set manually, Welcome to the IT help desk.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-play-prompt1.png)

1. Add a [Get customer input](get-customer-input.md) block and connect to the **Play prompt** block\.  
![\[The play prompt success branch connected to the Get customer input block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-get-customer-input3.png)

1. Choose the title of the [Get customer input](get-customer-input.md) block to open the properties page\.  
![\[The Get customer input block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-add-get-customer-input.png)

1.  Configure the **Get customer input** block, as shown in the following images\. Choose **Text\-to\-speech or chat text**, **Set manually**, and enter *How can I help* in the text box\. Set the **Interpret as** dropdown box to **Text**\.  
![\[The Properties page of the Get customer input block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input1.png)

   The following image shows the Amazon Lex tab\. Choose the name of your Amazon Lex bot from the dropdown list\. For **Alias** enter **$LATEST**\.  
![\[The Amazon Lex tab, the name and alias of the bot.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input2.png)

1. While still in the **Get customer input** block, choose **Add an intent**\.  
![\[The Intents section, the Add an intent option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input4.png)

1. Enter the names of the intents that you created in the Amazon Lex bot, such as PasswordReset and NetworkIssue\. They are case sensitive\!  
![\[The Intents section, the PasswordReset intent and NetworkIssue intent.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-configure-get-customer-input3.png)

1. Choose **Save**\.

1. Add a **Play prompt** block and connect it to the **PasswordReset** branch\. 

1. Choose the **Play prompt** title to open its properties page\. Configure the **Play prompt** block with the message *We’re putting you in a queue to help you with password reset\.* Choose **Save**\.

1. Add a second **Play prompt** block and connect it to the **NetworkIssue** branch\.

1. Choose the **Play prompt** title to open its properties page\. Configure the **Play prompt** block with the message *We’re putting you in a queue to help you with your network issues\.* Choose **Save**\.

1. Add a [Disconnect / hang up](disconnect-hang-up.md) block to the grid\. Connect the **Default** and **Error** branches to it\.

1. Add a [Set working queue](set-working-queue.md) block to the grid\. Connect the **Play prompt**\.

1. Choose the **Set working queue** title to open its properties page\. Configure the **Set working queue** block by using the drop\-down arrow to choose the **PasswordReset** queue\. Choose **Save**

1. Add a **Set working queue** block for NetworkIssue, and configure it with the NetworkIssue queue\.

1. Drag two **Transfer to queue** blocks \(from the **Terminate/Transfer** group\) onto the grid\.

1. Connect each of the **Set working queue** blocks to a **Transfer to queue** block\.

1. Drag another **Disconnect/hang up** block onto the grid\. Connect all of the remaining **Error** and **At capacity** branches to it\.

1. Choose **Save**, and then choose **Publish**\.  
![\[The Publish and Save buttons on the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-save-publish.png)
**Tip**  
Any blocks that aren't connected or configured correctly generate an error\. If this happens, double\-check that all branches are connected\.

1. When the flow publishes, it displays the message that it saved successfully\.  
![\[The message Contact flow saved successfully.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-contact-flow-published.png)

   If the flow doesn't save, double\-check that all the branches are connected to blocks\. That's the most common reason flows don't publish\. 