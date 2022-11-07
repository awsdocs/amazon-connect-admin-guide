# Part 2: Add intents to your Amazon Lex bot<a name="tutorial-lex-bot-intents"></a>

An intent is the action the user wants to perform\. In this part, add two intents to the bot\. Each intent represents a reason that users call the Help Desk: password reset and network issues\.

1. In the Amazon Lex console, in the **Intent details** section, enter **PasswordReset** as the name of your intent\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot4.png)

1. Scroll to the **Sample utterances** section\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-utterances.png)

1. Type **I forgot my password**, and then choose **Add utterance**\. Then add **reset my password** and choose **Add utterance** again\.

1. Choose **Save intent**\.

1. On the left navigation menu, choose **All intents list**\.

1. On the left navigation menu, choose **Back to intents list**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-bot-config3.png)

1. Choose **Add intent**, **Add empty intent**, and assign the name **NetworkIssue**\. Scroll down the page and add the following sample utterances:
   + **I can't access the internet**
   + **my email is down**

When you're done, go to [Part 3: Build and test the Amazon Lex bot](tutorial-lex-bot-build.md)\.