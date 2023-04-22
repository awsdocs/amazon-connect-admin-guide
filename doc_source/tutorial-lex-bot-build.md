# Part 3: Build and test the Amazon Lex bot<a name="tutorial-lex-bot-build"></a>

Build and test your bot to make sure that it works as intended before you publish it\.

1. In the Amazon Lex console, choose **Build**\. The build may take a minute or two\.  
![\[The Amazon Lex console, the Build button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot11.png)

1. When it's finished building, choose **Test**\.

1. Test the **PasswordReset** intent\. In the **Test Draft version** pane, type **I forgot my password**, and press **Enter**\.   
![\[The test draft version page, the box to enter an intent such as I forgot my password.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot12.png)

1. The verification looks like what's shown in the following image\.   
![\[The verification message from Amazon Lex, Intent PasswordReset is fullfilled.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot13.png)

1. To confirm that the **NetworkIssue** intent is working, type **my email is down**\. The verification looks like what's shown in the following image\.   
![\[The verification message from Amazon Lex, Intent NetworkIssue is fullfilled.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot14.png)

Go to [Step 2: Add permissions to Amazon Lex bot](tutorial1-add-permissions-for-bot.md)\.