# Use Amazon Lex and attributes<a name="attribs-cust-input-lex-bot"></a>

When you reference attributes in a **Get customer input** block, and choose Amazon Lex as the method of collecting the input, the attribute values are retrieved and stored from the output from the customer interaction with the Amazon Lex bot\. You can use an attribute for each intent or slot used in the Amazon Lex bot, as well as the sessions attributes associated with the bot\. An output branch is added to the block for each intent you include\. When a customer chooses an intent when interacting with the bot, the branch associated with that intent is followed in the flow\.

For a list of Amazon Lex attributes you can use and receive back from the Lex bot, see [Amazon Lex contact attributes](connect-attrib-list.md#attribs-lex-table)\.

# Using an Amazon Lex bot to get customer input

1. Open an existing or create a new flow\.

1. Under **Interact**, drag a **Get customer input** block to the designer\.

1. Choose the title of the block to display the block settings, then select **Text to speech \(Ad hoc\)**\.

1. Choose **Enter text**, then enter text in the **Enter text to be spoken** field that is used as a message or greeting to your customers\. For example, "Thank you for calling" followed by a request to enter information to fulfill the intents you defined in your Amazon Lex bot\.

1. Choose the **Amazon Lex** tab, then from the drop\-down menu, choose the Amazon Lex bot to use to get customer input\.

1. By default, the **Alias** field is populated with $LATEST\. To use a different alias of the bot, enter the alias value to use\.
**Important**  
In a production environment, always use a different alias than **TestBotAlias** for Amazon Lex and **$LATEST** for Amazon Lex classic\. **TestBotAlias** and **$LATEST** support a limited number of concurrent calls to an Amazon Lex bot\. For more information, see [Runtime Service Quotas](https://docs.aws.amazon.com/lexv2/latest/dg/gl-limits.html#gl-limits-runtime) or [Runtime Service Quotas \(Amazon Lex Classic\)](https://docs.aws.amazon.com/lex/latest/dg/gl-limits.html#gl-limits-runtime)\.

1. Optionally, to pass an attribute to Amazon Lex to use as a session attribute, choose **Add an attribute**\. Specify the value to pass using either text or an attribute\.

1. To create a branch from the block based on the customer intent, choose **Add an intent**, then enter the name of the intent exactly the same as the intent name in your bot\.

1. Choose **Save**\.