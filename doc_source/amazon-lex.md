# Add an Amazon Lex Bot<a name="amazon-lex"></a>

In this article we guide you through the steps to add a Amazon Lex bot to Amazon Connect\. 

With Amazon Lex, you can build conversational interactions \(bots\) that feel natural to your customers\. Amazon Connect with Amazon Lex bots can also capture customer input as digits that customers enter on their numeric keypad when used in an Amazon Connect contact flow\. This way customers can choose how they want to enter sensitive information such as account numbers\. 

To follow along with this walkthrough, you need the following: 
+ An active AWS account\. 
+ An Amazon Connect instance created in the US East \(N\. Virginia\) Region\. After you create your instance, claim a phone number for it\.

## Create an Amazon Lex Bot<a name="lex-bot-create"></a>

In this step you'll create a custom bot to demonstrate the Press or Say integration with Amazon Connect\. The bot prompts callers to press or say a number that matches the menu option for the task to complete\. In this case, the input is checking their account balance\.

1. Open the [Amazon Lex console\.](https://console.aws.amazon.com/lex/)

1. If you are creating your first bot, choose **Get Started**\. Otherwise, choose **Bots, Create**\.

1. On the **Create your Lex bot** page, choose **Custom bot** and provide the following information:
   + **Bot name **– For this walkthrough, name the bot **AccountBalance**\.
   + **Output voice**– Select the voice for your bot to use when speaking to callers\. The default voice for Amazon Connect is Joana\.
   + **Session timeout**– Choose how long the bot should wait to get input from a caller before ending the session\.
   + **COPPA**– Choose whether the bot is subject to the Child Online Privacy Protection Act\.

1. Choose **Create**\.

## Configure the Amazon Lex Bot<a name="lex-bot-configure"></a>

In this step you'll determine how the bot responds to customers by providing intents, sample utterances, slots for input, and error handling\.

### Create Intents<a name="lex-bot-create-intents"></a>

For this example, you'll configure the bot with two intents: one to look up account information, and another to speak with an agent\.

1. In the Amazon Lex console choose the **\+** icon next to **Intents**, and choose **Create new intent**\.

1. Name the intent **AccountLookup**\.

1. Create another intent, and name it **SpeakToAgent**\.

### Add Sample Utterances<a name="lex-bot-add-utterances"></a>

After defining the intents, add some sample utterances\.

1. Select the **AccountLookup** intent\.

1. Add a sample utterance, such as *Check my account balance*, and choose the **\+** icon\.

1. Add a second utterance, such as *One* and choose the **\+** icon\. This assigns the utterance of “one” or key press of “1” to the **AccountLookup** intent\.
**Tip**  
You must add an utterance of "one" in the bot, and not the number "1"\. This is because Amazon Lex doesn't support numeric input directly\. To get around this, later in this walkthrough you'll use numeric input to interact with a Lex bot invoked from a contact flow\. 

1. Select **SpeakToAgent**\.

1. Add a sample utterance, such as *Speak to an agent*, and choose **\+**\.

1. Add a second utterance, such as *Two*, and choose **\+**\.

### Add Slots<a name="lex-bot-add-slots"></a>

Before the bot can respond with the caller’s account balance, it needs the account number\.

1. Choose the **AccountLookup** intent\.

1. Under **Slots**, add a slot named **AccountNumber**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-slots.png)

1. For **Slot type**, use the drop\-down to choose **AMAZON\.NUMBER**\.

1. For **Prompt**, add the text to be spoken when the call is answered\. For example, ask callers to enter their account number using their keypad: *Using your touch\-tone keypad, please enter your account number*\.

1. Choose the \+ icon\.

1. Make sure that the **Required **check box is selected\.

### Add Responses<a name="lex-bot-add-responses"></a>

Now that you have intents, utterances, and a slot, add the responses that the bot provides to callers\. Because you are creating a simple bot for this example, you are not hooking up the bot to look up real customer data\. The example bot responds with text strings that you add, regardless of the account number that a caller provides\.

1. Select the **AccountLookup** intent\.

1. In the **Response** section, add a message for the bot to say to customers\. For example, “The balance for your account is $2,586\.34\.”

1. Choose **Save Intent**\.

1. For the **SpeakToAgent** intent, add a message that lets callers know that their call is being connected to an agent\. For example, “Okay, an agent will be with you shortly\.”

1. Choose **Save Intent**\.

## Build and Test the Amazon Lex Bot<a name="lex-bot-build"></a>

After you create your bot, make sure it works as intended before you publish it\.

1. Choose **Build**\. It may take a minute or two\.

1. When it's finished building, choose **Test Chatbot**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-test-chatbot.png)

1. Let's test the **AccountLookup** intent: In the **Test Chatbot** pane, in the **Chat with your bot** box, type **1**\. Then type a fictitous account number\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-test-run.png)

1. Choose **Clear chat history**\. 

1. To confirm that the **SpeakToAgent** intent is working, type **2**\.

## Publish the Amazon Lex Bot and Create an Alias<a name="lex-bot-publish"></a>

Next, publish the bot so that you can add it to a contact flow in Amazon Connect\.

1. Choose **Publish**\.

1. Provide an alias for your bot\. Use the alias to specify this version of the bot in the contact flow, for example, Test\.

1. Choose **Publish**\.

## Add the Amazon Lex Bot to an Amazon Connect Instance<a name="lex-bot-add-to-connect"></a>

Before you can use a bot in your contact flow you need to add it to your Amazon Connect instance\. You can only add bots created under the same AWS account\. 

If you add Amazon Lex bots created in a different Region from your instance, performance may be affected\.

1. Open the [Amazon Connect console\.](https://console.aws.amazon.com/connect/)

1. Select the **Instance Alias** of the instance to which to add the bot\.

1. Choose **Contact flows**\.

1. Under **Amazon Lex**, use the drop\-down to choose a name for your bot and then choose **\+ Add Lex Bot**\.

1. Select the **AccountBalance** bot and choose **Save Lex Bots**\. If the name of your bot doesn't appear in the list, reload the page to get it to show up\.

## Create a Contact Flow and Add Your Amazon Lex Bot<a name="lex-bot-create-flow-add-bot"></a>

Next, create a new contact flow that uses your Amazon Lex bot\. When you create the contact flow, you configure the message played to callers\.

1. Log in to your Amazon Connect instance with an account that has permissions for contact flows and Amazon Lex bots\.

1. Choose **Routing, Contact flows, Create contact flow**, and type a name for the flow\.

1. Under **Interact**, drag a **Get customer input ** block onto the designer, and connect it to the **Entry point block**\.

1. Click the **Get customer input** block to open it\. Choose **Text to speech \(Ad hoc\), Enter text**\.

1. Type a message that provides callers with information about what they can do\. For example, use a message that matches the intents used in the bot, such as “To check your account balance, press or say 1\. To speak to an agent, press or say 2\.”  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-get-customer-input.png)

### Add the Amazon Lex Bot to Your Contact Flow<a name="lex-bot-add-to-flow"></a>

In this step you'll specify the bot as the method of getting customer input\.

1. In the **Get customer input** block select **Amazon Lex**\.

1. For **Name**, use **AccountBalance**\. For **Alias**, use **Test**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-get-customer-input2.png)

1. Under **Intents**, choose **Add an intent**\.

1. Type **AccountLookup** and choose **Add another intent**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-get-customer-input3.png)

1. Type **SpeakToAgent** and choose **Save**\.

### Finish the Contact Flow<a name="lex-bot-finish-flow"></a>

After the caller interacts with the bot, finish the contact flow to complete the call for the customer\.

1. If the caller presses 1 to get their account balance, use a **Prompt** block to play a message and disconnect the call\.

1. If the caller presses 2 to speak to an agent, use a **Set queue** block to set the queue and transfer the caller to the queue, which ends the contact flow\.

To complete the **AccountLookup** intent:

1. Under **Interact**, drag a **Play prompt block** to the designer, and connect the **AccountLookup** node of the **Get customer input** block to it\. After the customer gets their account balance from the Amazon Lex bot, the message in the **Play prompt** block plays\.

1. Under **Terminate/Transfer**, drag a **Disconnect/hang up** block to the designer, and connect the **Play prompt** block to it\. After the prompt message plays, the call is disconnected\.

To complete the **SpeakToAgent** intent:

1. Add a **Set customer queue** block and connect it to the **SpeakToAgent** node of the **Get customer input** block\.

1. Add a **Transfer to queue** block\. 

1. Connect the Success node of the **Set customer queue** block to the **Transfer queue**\.

1. Choose **Save**, then **Publish**\.

Your finished contact flow will look something like the following one:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/lex-contactflow-designer.png)

## Assign the Contact Flow to a Phone Number<a name="lex-bot-assign-number"></a>

When callers call in to your contact center, the contact flow to which they are sent is the one assigned to the telephone number that they dialed\. To make the new contact flow active, assign it to a phone number for your instance\.

1. Open the Amazon Connect Dashboard\.

1. Choose **View phone numbers**\.

1. Select the phone number to which to assign the contact flow\.

1. Add a description\.

1. In the **Contact flow/IVR** menu, choose the contact flow that you just created\.

1. Choose **Save**\.

## Try It\!<a name="lex-bot-try-it"></a>

To try the bot and contact flow, call the number you assigned to the contact flow\. Follow the prompts\. 