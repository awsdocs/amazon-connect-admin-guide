# How to use Lex session attributes<a name="how-to-use-session-attributes"></a>

When a customer starts a conversation with your bot, Amazon Lex creates a *session*\. With *session attributes*, also known as *Lex attributes*, you can pass information between the bot and Amazon Connect during the session\. For a list of Amazon Lex attributes you can use, see [Amazon Lex contact attributes](connect-attrib-list.md#attribs-lex-table)\.

## Life cycle of session attributes<a name="session-attribute-lifecycle"></a>

There's one set of session attributes per conversation\. In cases where a Lambda is invoked to do some processing, following is the order of precedence:
+ Service defaults: these attributes are only used if no attributes are defined\.
+ Session attributes provided by Amazon Connect: these attributes are defined in the [Get customer input](get-customer-input.md) block\.
+ Session attributes provided by Lambda override everything prior: When a Lambda function is invoked and it does some processing, it overrides any session attributes set in the [Get customer input](get-customer-input.md) block\.

Let's say a customer utters that they want **a car**\. That's the first session attribute to go through processing\. When asked what kind of car, they say **luxury car**, this second utterance overrides any Lambda processing that took place on the first utterance\. 

For an example of how to create a Lambda function that processes session attributes, see [Step 1: Create a Lambda Function](https://docs.aws.amazon.com/lex/latest/dg/gs2-prepare.html) in the *Amazon Lex Developer Guide*\.

For the structure of the event data that Amazon Lex provides to a Lambda function, see [Lambda Function Input Event and Response Format](https://docs.aws.amazon.com/lex/latest/dg/lambda-input-response-format.html) in the *Amazon Lex Developer Guide*\.

## Contact blocks that support Lex session attributes<a name="blocks-support-lex-session-attributes"></a>

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

### More information<a name="more-info-attributes"></a>

For more information about using Amazon Lex session attributes, see [Managing Conversation Context](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html) in the *Amazon Lex Developer Guide*\.