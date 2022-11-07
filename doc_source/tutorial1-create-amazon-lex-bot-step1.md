# Part 1: Create an Amazon Lex bot<a name="tutorial1-create-amazon-lex-bot-step1"></a>

This step assumes it's the first time you've opened the Amazon Lex console\. If you've created a Amazon Lex bot before, your steps differ slightly from the ones in this section\.

1. Choose the following link to open the Amazon Lex console, or enter the URL in your web browser: **[https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)**\.

1. If this is the first time you've created Amazon Lex bot, choose **Get Started**\. Otherwise, you're already in the Amazon Lex dashboard\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-console1.png)

1. Choose **Create a blank bot**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-lex-custom-bot.png)

1. Enter the following information:
   + **Bot name **— For this tutorial, name the bot **HelpDesk**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-bot-config1.png)
   + IAM permissions: Choose **Create a role with basic Amazon Lex permissions**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-iam-permissions.png)
   + **COPPA**— Choose whether the bot is subject to the [Children's Online Privacy Protection Act](https://www.ftc.gov/enforcement/rules/rulemaking-regulatory-reform-proceedings/childrens-online-privacy-protection-rule)\.
   + **Idle session timeout**— Choose how long the bot should wait to get input from a caller before ending the session\.

1. Choose **Next**\.

1. On the **Add language to bot** page, choose the language and voice for your bot to use when speaking to callers\. The default voice for Amazon Connect is Joanna\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tutorial1-bot-config2.png)

1. Choose **Done**\.

Go to [Part 2: Add intents to your Amazon Lex bot](tutorial-lex-bot-intents.md)\.