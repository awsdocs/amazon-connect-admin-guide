# How to use Lex session attributes<a name="how-to-use-session-attributes"></a>

When a customer starts a conversation with your bot, Amazon Lex creates a *session*\. With *session attributes*, also known as *Lex attributes*, you can pass information between the bot and Amazon Connect during the session\.

You can use Lex session attributes in the following blocks when a Lex bot is called:
+ Get customer input
+ Set contact attributes
+ Set hold flow
+ Set working queue
+ Set customer queue flow
+ Set disconnect flow
+ Set logging behavior
+ Set callback number
+ Set whisper flow
+ Change routing priority/age
+ Check contact attributes
+ Loop
+ Wait
+ Invoke AWS Lambda function
+ Transfer to phone number
+ Transfer to flow

## More information<a name="more-info-attributes"></a>

For more information about using Amazon Lex session attributes, see [Managing Conversation Context](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html) in the *Amazon Lex Developer Guide*\.