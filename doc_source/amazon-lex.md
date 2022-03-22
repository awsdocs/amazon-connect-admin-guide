# Add an Amazon Lex bot<a name="amazon-lex"></a>

In this article we guide you through the steps to add an Amazon Lex bot to Amazon Connect\. 

With Amazon Lex, you can build conversational interactions \(bots\) that feel natural to your customers\. Amazon Connect with Amazon Lex bots can also capture customer input as digits that customers enter on their numeric keypad when used in an Amazon Connect contact flow\. This way customers can choose how they want to enter sensitive information such as account numbers\. 

To follow along with this walkthrough, you need the following: 
+ An active AWS account\. 
+ An Amazon Connect instance\. 

**Tip**  
You can also use Amazon Lex to power interactive messages for Amazon Connect chat\. Interactive messages are rich messages that present a prompt and pre\-configured display options that a customer can select from\. These messages are powered by Amazon Lex and configured through Amazon Lex using a Lambda\. For more information, see [Add interactive messages to chat](interactive-messages.md)\.

## Create an Amazon Lex bot<a name="lex-bot-create"></a>

In this step you'll create a custom bot to demonstrate the Press or Say integration with Amazon Connect\. The bot prompts callers to press or say a number that matches the menu option for the task to complete\. In this case, the input is checking their account balance\.

------
#### [ Amazon Lex ]

1. Open the [Amazon Lex console\.](https://console.aws.amazon.com/lexv2/home)

1. Choose **Create bot**\.

1. On the **Configure bot settings** page, choose **Create \- Create a blank bot** and provide the following information:
   + **Bot name** — For this walkthrough, name the bot **AccountBalance**\.
   + **IAM permissions** — Select a role if you have one created\. Otherwise, choose **Create a role with basic Amazon Lex permissions**\.
   + **COPPA** — Choose whether the bot is subject to the Child Online Privacy Protection Act\.
   + **Session timeout** — Choose how long the bot should wait to get input from a caller before ending the session\.

1. Choose **Next**\.

1. Provide language and voice specific information:
   + **Language** — Select language and locale from the list of [Languages and locales supported by Amazon Lex](https://docs.aws.amazon.com/lexv2/latest/dg/how-languages.html)\. 
   + **Voice interaction** — Select the voice for your bot to use when speaking to callers\. The default voice for Amazon Connect is Joanna\.

1. Choose **Done**\. The AccountBalance bot is created, and the **Intent** page is displayed\.

------
#### [ Amazon Lex \(Classic\) ]

1. Open the [Amazon Lex console\.](https://console.aws.amazon.com/lex/)

1. If you are creating your first bot, choose **Get Started**\. Otherwise, choose **Bots, Create**\.

1. On the **Create your bot** page, choose **Custom bot** and provide the following information:
   + **Bot name** — For this walkthrough, name the bot **AccountBalance**\.
   + **Output voice** — Select the voice for your bot to use when speaking to callers\. The default voice for Amazon Connect is Joanna\.
   + **Session timeout** — Choose how long the bot should wait to get input from a caller before ending the session\.
   + **COPPA** — Choose whether the bot is subject to the Child Online Privacy Protection Act\.

1. Choose **Create**\.

------

## Configure the Amazon Lex bot<a name="lex-bot-configure"></a>

In this step you'll determine how the bot responds to customers by providing intents, sample utterances, slots for input, and error handling\.

For this example, you'll configure the bot with two intents: one to look up account information, and another to speak with an agent\.

### Create AccountLookup intent<a name="lex-bot-create-account-lookup-intent"></a>

------
#### [ Amazon Lex ]

1. After you created the bot, you are on the **Intents** page the Amazon Lex console\. If you're not there, you can get there by choosing **Bots**, **AccountBalance**, **Bot versions**, **Draft version**, **Intents**\. Choose **Add intent**, **Add empty intent**\.

1. In the **Intent name** box, enter **AccountLookup**\.

1. Scroll down the page to **Sample utterances**\. In this step you enter utterances that allow the customer to elicit the AccountLookup intent\. Enter the following utterances, and choose **Add utterance** after each one\. 
   + **Check my account balance**
   + **One**: This assigns the utterance of “one” or key press of “1” to the **AccountLookup** intent\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-enter-utterances.png)

1. Scroll to the **Slots** section, and choose **Add slot**\. Complete the box as follows:

   1. **Required for this intent** = selected\.

   1. **Name** = **AccountNumber**\. 

   1. **Slot type** = **AMAZON\.Number**\. 

   1. **Prompts** = the text to be spoken when the call is answered\. For example, ask callers to enter their account number using their keypad: **Using your touch\-tone keypad, please enter your account number**\. Choose **Add**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-add-slots.png)

1. Scroll to the **Closing responses** section\. Add a message for the bot to say to customers\. For example, **Your account balance is $1,234\.56**\. \(For this walkthrough, we aren't going to actually get the data, which is what you would do in reality\.\)  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-response1.png)

1. Choose **Save intent**\.

------
#### [ Amazon Lex \(Classic\) ]

1. In the Amazon Lex console choose the **\+** icon next to **Intents**, and choose **Create new intent**\.

1. Name the intent **AccountLookup**\.

1. Add a sample utterance, such as *Check my account balance*, and choose the **\+** icon\.

1. Add a second utterance, such as *One* and choose the **\+** icon\. This assigns the utterance of “one” or key press of “1” to the **AccountLookup** intent\.
**Tip**  
You must add an utterance of "one" in the bot, and not the number "1"\. This is because Amazon Lex doesn't support numeric input directly\. To get around this, later in this walkthrough you'll use numeric input to interact with a Lex bot invoked from a contact flow\. 

1. Under **Slots**, add a slot named **AccountNumber**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-slots.png)

1. For **Slot type**, use the drop\-down to choose **AMAZON\.NUMBER**\.

1. For **Prompt**, add the text to be spoken when the call is answered\. For example, ask callers to enter their account number using their keypad: *Using your touch\-tone keypad, please enter your account number*\.

1. Choose the \+ icon\.

1. Make sure that the **Required **check box is selected\.

1. In the **Response** section, add a message for the bot to say to customers\. For example, **Your account balance is $1,234\.56**\. 

1. Choose **Save Intent**\.

------

### Create SpeakToAgent intent<a name="lex-bot-create-speaktoagent-intent"></a>

------
#### [ Amazon Lex ]

1. Navigate to the **Intents** page: choose **Back to intents list**\. 

1. Choose **Add intent**, **Add empty intent**\. 

1. In the **Intent name** box, enter **SpeakToAgent**, and then choose **Add**\. 

1. Scroll down to **Sample utterances** section\. Enter the following utterances, which allow the customer to elicit the SpeakToAgent intent:
   + **Speak to an agent**
   + **Two**

1. Scroll down to the **Closing responses** section\. Add a message for the bot to say to customers\. For example, **Okay, an agent will be with you shortly**\.

1. Choose **Save intent**\.

------
#### [ Amazon Lex \(Classic\) ]

1. In the Amazon Lex console choose the **\+** icon next to **Intents**, and choose **Create new intent**\.

1. Name the intent **SpeakToAgent**\.

1. Select **SpeakToAgent**\.

1. Add a sample utterance, such as *Speak to an agent*, and choose **\+**\.

1. Add a second utterance, such as *Two*, and choose **\+**\.

1. Add a message that lets callers know that their call is being connected to an agent\. For example, “Okay, an agent will be with you shortly\.”

1. Choose **Save Intent**\.

------

## Build and test the Amazon Lex bot<a name="lex-bot-build"></a>

After you create your bot, make sure it works as intended\.

------
#### [ Amazon Lex ]

1. At the bottom of the page, choose **Build**\. It may take a minute or two\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-build-test-intent.png)

1. When it's finished building, choose **Test**\.

1. Let's test the **AccountLookup** intent: In the **Test Draft version** pane, in the **Type a message** box, type **1** and press Enter\. Then type a fictitous account number and press Enter\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-test1.png)

   1. Clear the test box\.

   1. Type the intents you want to test\.

1. To confirm that the **SpeakToAgent** intent is working, clear the test box, and then type **2** and press Enter\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-test2.png)

1. Close the **Test Draft version** pane\.

------
#### [ Amazon Lex \(Classic\) ]

1. Choose **Build**\. It may take a minute or two\.

1. When it's finished building, choose **Test Chatbot**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-test-chatbot.png)

1. Let's test the **AccountLookup** intent: In the **Test Chatbot** pane, in the **Chat with your bot** box, type **1**\. Then type a fictitous account number\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-test-run.png)

1. Choose **Clear chat history**\. 

1. To confirm that the **SpeakToAgent** intent is working, type **2**\.

------

## Create a bot version \(Optional\)<a name="lex-bot-create-bot-version"></a>

In this step you create a new bot version to use in an alias\. It's how you create an alias that can be used in a production environment\. Test aliases are subject to lower throttling limits\. Although this is a test walkthrough, creating a version is a best practice\.

------
#### [ Amazon Lex ]

1. If you're on the **Intents** page, choose **Back to intents list**\.

1. On the left menu, choose **Bot versions**\.

1. Choose **Create version**\.

1. Review the details of the **AccountBalance** bot, and then choose **Create**\.

   This creates a version of your bot \(Version 1\)\. to associate a version directly with an alias\. You can switch versions on an non\-test alias without having to track which version is getting published\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-version1.png)

------

## Create an alias for the bot<a name="lex-bot-create-alias"></a>

------
#### [ Amazon Lex ]

1. In the left menu, choose **Aliases**\.

1. On the **Aliases** page, choose **Create alias**\.

1. In the **Alias name** box, enter a name, such as **Test**\. Later in this walkthrough you'll use this alias to specify this version of the bot in your contact flow\. 
**Important**  
In a production environment, always use a different alias than **TestBotAlias** for Amazon Lex and **$LATEST** for Amazon Lex classic\. **TestBotAlias** and **$LATEST** support a limited number of concurrent calls to an Amazon Lex bot\. For more information, see [Runtime Service Quotas](https://docs.aws.amazon.com/lexv2/latest/dg/gl-limits.html#gl-limits-runtime)\.

1. For **Associated version**, choose the version you just created, such as **Version 1**\. 

1. Choose **Create**\.

------
#### [ Amazon Lex \(Classic\) ]

1. Choose **Publish**\.

1. Provide an alias for your bot\. Use the alias to specify this version of the bot in the contact flow, for example, **Test**\.
**Important**  
In a production environment, always use a different alias than **TestBotAlias** for Amazon Lex and **$LATEST** for Amazon Lex classic\. **TestBotAlias** and **$LATEST** support a limited number of concurrent calls to an Amazon Lex bot\. For more information, see [Runtime Service Quotas](https://docs.aws.amazon.com/lex/latest/dg/gl-limits.html#gl-limits-runtime)\.

1. Choose **Publish**\.

------

## Add the Amazon Lex bot to your Amazon Connect instance<a name="lex-bot-add-to-connect"></a>

------
#### [ Amazon Lex ]

1. Open the [Amazon Connect console\.](https://console.aws.amazon.com/connect/)

1. Select the Amazon Connect instance that you want to integrate with your Amazon Lex bot\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance-alias2.png)

1. On the navigation menu, choose **Contact flows**\.

1. Under **Amazon Lex**, use the dropdown to select the Region of your Amazon Lex bot, and then select your Amazon Lex bot, **AccountBalance**\. 

1. Select the Amazon Lex bot alias name from the dropdown \(**Test**\), and then choose **\+ Add Lex Bot**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-region-bot.png)

**Note**  
Amazon Connect uses Amazon Lex resource\-based policies to make calls to your Amazon Lex bot\. When you associate an Amazon Lex bot with your Amazon Connect instance, the resource\-based policy on the bot is updated to give Amazon Connect permission to invoke the bot\. For more information on Amazon Lex resource\-based policies, see [How Amazon Lex works with IAM](https://docs.aws.amazon.com/lexv2/latest/dg/security_iam_service-with-iam.html#security_iam_service-with-iam-resource-based-policies)\.

------
#### [ Amazon Lex \(Classic\) ]

1. Open the [Amazon Connect console\.](https://console.aws.amazon.com/connect/)

1. Select the Amazon Connect instance that you want to integrate with your Amazon Lex bot\.

1. On the navigation menu, choose **Contact flows**\.

1. Under **Amazon Lex**, select the Region of your Amazon Lex classic bot from the dropdown, and then select your Amazon Lex classic bot\. It’s name will have the suffix “\(Classic\)”\. Then choose **Add Lex Bot**\.

------

## Create a contact flow and add your Amazon Lex bot<a name="lex-bot-create-flow-add-bot"></a>

**Important**  
If you're using an Amazon Lex V2 bot, your language attribute in Amazon Connect must match the language model used to build your Lex bot\. This is different than Amazon Lex \(Classic\)\. Use a [Set voice](set-voice.md#set-voice-lexv2bot) block to indicate the Amazon Connect language model, or use a [Set contact attributes](set-contact-attributes.md) block\.

Next, create a new contact flow that uses your Amazon Lex bot\. When you create the contact flow, you configure the message played to callers\.

1. Log in to your Amazon Connect instance with an account that has permissions for contact flows and Amazon Lex bots\.

1. On the navigation menu, choose **Routing, Contact flows, Create contact flow**, and type a name for the flow\.

1. Under **Interact**, drag a [Get customer input](get-customer-input.md) block onto the designer, and connect it to the **Entry point block**\.

1. Click the **Get customer input** block to open it\. Choose **Text to speech or chat text, Enter text**\.

1. Type a message that provides callers with information about what they can do\. For example, use a message that matches the intents used in the bot, such as “To check your account balance, press or say 1\. To speak to an agent, press or say 2\.”  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-get-customer-input.png)

1. Select the **Amazon Lex** tab\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lexv2-get-customer-input2.png)

1. In the **Name** dropdown, select the **AccountBalance** bot you created earlier\. 

   1. If you selected an Amazon Lex bot, under **Alias** use the dropdown menu to select the bot alias, **Test**\. from 

   1. Amazon Lex Classic bots have the suffix "\(Classic\)" appended to their names\. If you have selected a Classic bot, enter the alias you want to use in the **Alias** field\.

   1. For Amazon Lex bots, you also have the option of manually setting a bot alias ARN\. Choose **Set manually**, then either type the ARN of the bot alias you want to use or set the ARN using a dynamic attribute\.

1. Under **Intents**, choose **Add an intent**\.

1. Type **AccountLookup** and choose **Add another intent**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-get-customer-input3.png)

1. Type **SpeakToAgent** and choose **Save**\.

### Finish the contact flow<a name="lex-bot-finish-flow"></a>

In this step you finish adding parts to the contact flow that run after the caller interacts with the bot:

1. If the caller presses 1 to get their account balance, use a **Prompt** block to play a message and disconnect the call\.

1. If the caller presses 2 to speak to an agent, use a **Set queue** block to set the queue and transfer the caller to the queue, which ends the contact flow\.

Here are the steps to create the contact flow:

1. Under **Interact**, drag a **Play prompt block** to the designer, and connect the **AccountLookup** node of the **Get customer input** block to it\. After the customer gets their account balance from the Amazon Lex bot, the message in the **Play prompt** block plays\.

1. Under **Terminate/Transfer**, drag a **Disconnect** block to the designer, and connect the **Play prompt** block to it\. After the prompt message plays, the call is disconnected\.

To complete the **SpeakToAgent** intent:

1. Add a **Set working queue** block and connect it to the **SpeakToAgent** node of the **Get customer input** block\.

1. Add a **Transfer to queue** block\. 

1. Connect the Success node of the **Set customer queue flow** block to the **Transfer queue**\.

1. Choose **Save**, then **Publish**\.

Your finished contact flow will look something like the following one:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-contactflow-designer.png)

**Tip**  
If your business uses multiple locales in a single bot, add a [Set contact attributes](set-contact-attributes.md) block to the beginning of your flow\. Configure this block to use the [$\.LanguageCode](connect-attrib-list.md#attribs-system-table) system attribute\. 

## Assign the contact flow to a phone number<a name="lex-bot-assign-number"></a>

When customers call in to your contact center, the contact flow to which they are sent is the one assigned to the telephone number that they called\. To make the new contact flow active, assign it to a phone number for your instance\.

1. Open the Amazon Connect console\.

1. Choose **Routing, Phone numbers**\.

1. On the **Manage Phone numbers** page, select the phone number to assign to the contact flow\.

1. Add a description\.

1. In the **Contact flow/IVR** menu, choose the contact flow that you just created\.

1. Choose **Save**\.

## Try it\!<a name="lex-bot-try-it"></a>

To try the bot and contact flow, call the number you assigned to the contact flow\. Follow the prompts\. 