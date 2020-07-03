# How to reference contact attributes<a name="how-to-reference-attributes"></a>

The way you reference contact attributes depends on how they were created and how you are accessing them\. To reference attributes in the same namespace, such as a system attribute, you use the attribute name, or the name you specified as the **Destination key**\. To reference values in a different namespace, such as referencing an external attribute, you specify the JSONPath syntax to the attribute\.

For example, to reference a customer name from a Lambda function lookup, you use $\.External\.AttributeKey, replacing AttributeKey with the key \(or name\) of the attribute returned from the Lambda function\. To reference an attribute from an Amazon Lex bot, you use the format $\.Lex\. and then include the part of the Amazon Lex bot to reference, such as $\.Lex\.IntentName\. To reference the customer input to an Amazon Lex bot slot, use $\.Lex\.Slots\.*slotName*, replacing *slotName* with the name of the slot in the bot\.

To reference user\-defined attributes, such as those set with the **Set contact attributes** block, use the drop\-down menus in subsequent blocks to reference the attribute, or use the Attributes namespace in JSONPath to the attribute if used in a text field\. For example, if you create a user\-defined attribute in a **Set contact attributes** block, you reference it in one of the following ways:
+ In a block that supports attributes, such as a **Check contact attributes** block, choose **User Defined** for the **Type**, and use the value you entered for the **Destination key** in the **Attribute** field\.
+ In a text field in a block, such as a **Play prompt** block, use the JSONPath $\.Attributes\.DestinationKey, replacing DestinationKey with the value you entered in the **Destination key**\.

JSONPath is a standardized way to query elements of a JSON object\. JSONPath uses path expressions to navigate elements, nested elements, and arrays in a JSON document\. For more information about JSON, see [Introducing JSON](http://www.json.org/)\.

## Checking attribute values in a Check contact attributes block<a name="check-contact-attrib-block"></a>

When you include a **Check contact attributes** block in a contact flow, it checks the value of the attribute you specify\. You then add a condition to compare the value of the attribute to, such as "greater than" or "contains\." For each condition you add, an output branch is added to the block\. You can then route the contact based on the conditions by connecting the output branch for the condition to the next block in the contact flow\. For example, you can check the current number of customers in a queue, then route the contact to the queue if the active contacts are fewer than 5\. You can also route the contact to another different queue if the number of active contacts is more than 5\. You can use whichever metrics or attributes you want to make routing decisions as appropriate for your needs\. The following procedure describes how to check for the number of contacts in a queue and then route the contact to a queue that has fewer than 5 active contacts in it\.

## Using a Check contact attributes block to route a contact to a queue

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Open an existing contact flow or create a new one\.

1. Optionally, under **Interact**, add a **Play prompt** block to the designer to play a greeting to your customers\. Add a connector between the **Entry point** block and the **Play prompt** block\.

1. Under **Set**, drag a **Get queue metrics** block to the designer, and connect the **Okay** branch of the **Play prompt** block to it\.

1. Choose the title of the **Get queue metrics** block to open the properties for the block\. By default, the block retrieves metrics for the current working queue\. To retrieve metrics for a different queue, choose **Set queue**\.

1. Choose **Select a queue**, then select the queue to retrieve metrics for from the drop\-down, then choose **Save**\.

   You can also determine which queue to retrieve metrics for using contact attributes\.

1. Under **Branch**, drag a **Check contact attributes** block to the designer\.

1. Choose the title of the block to display the settings for the block\. Then, under **Attribute to check**, select **Queue metrics** in the **Type** drop\-down menu\.

1. Under **Attribute**, choose **Contacts in queue**\.

1. To use conditions to route the contact, choose **Add another condition**\.

   By default, the **Check contact attributes** block includes a single condition, **No match**\. The **No match** branch is followed when there are no matches for any of the conditions you define in the block\.

1. Under **Conditions to check**, select **Is less than** as the operator for the condition in the drop\-down menu, then in the value field enter 5\.

1. Choose **Add another condition**, then choose **Is greater or equal** from the drop\-down menu, and enter 5 in the value field\.

1. Choose **Save**\.

   You now see two new output branches for the **Check contact attributes** block\.

You can now add additional blocks to the contact flow to route the contact as desired\. For example, connect the < 5 branch to a **Transfer to queue** block to transfer calls to the queue when there are fewer than five calls currently in the queue\. Connect the > 5 branch to a Set customer callback number block and then transfer the call to a callback queue using a **Transfer to queue** block so the customer doesn't have to stay on hold\.

## Referencing attributes from a Play prompt block<a name="attribs-play-prompt"></a>

Use a **Play prompt** block to use an audio file to play as a greeting or message to callers\. You can also use contact attributes to specify the greeting or message delivered to callers\. To use the values of a contact attribute to personalize a message for a customer, include references to stored or external contact attributes in the text\-to\-speech message\. For example, if you retrieved the customer’s name from a Lambda function, and it returns values from your customer database for FirstName and LastName, you could use these attributes to say the customer’s name in the text\-to\-speech block by including text similar to the following:

Hello $\.External\.FirstName $\.External\.LastName, thank you for calling\.

Alternatively, you could store the attributes returned from the Lambda function using a **Set contact attributes** block, and then reference the user\-defined attribute created in the text to speech string\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-attribute.png)

## Getting customer input using an Amazon Lex bot<a name="attribs-cust-input-lex-bot"></a>

When you reference attributes in a **Get customer input** block, and choose Amazon Lex as the method of collecting the input, the attribute values are retrieved and stored from the output from the customer interaction with the Amazon Lex bot\. You can use an attribute for each intent or slot used in the Amazon Lex bot, as well as the sessions attributes associated with the bot\. An output branch is added to the block for each intent you include\. When a customer chooses an intent when interacting with the bot, the branch associated with that intent is followed in the contact flow\.

## Using an Amazon Lex bot to get customer input

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Open an existing or create a new contact flow\.

1. Under **Interact**, drag a **Get customer input** block to the designer\.

1. Choose the title of the block to display the block settings, then select **Text to speech \(Ad hoc\)**\.

1. Choose **Enter text**, then enter text in the **Enter text to be spoken** field that is used as a message or greeting to your customers\. For example, "Thank you for calling" followed by a request to enter information to fulfill the intents you defined in your Amazon Lex bot\.

1. Choose the **Amazon Lex** tab, then from the drop\-down menu, choose the Amazon Lex bot to use to get customer input\.

1. By default, the **Alias** field is populated with $LATEST\. To use a different alias of the bot, enter the alias value to use\.

1. Optionally, to pass an attribute to Amazon Lex to use as a session attribute, choose **Add an attribute**\. Specify the value to pass using either text or an attribute\.

1. To create a branch from the block based on the customer intent, choose **Add an intent**, then enter the name of the intent exactly the same as the intent name in your bot\.

1. Choose **Save**\.