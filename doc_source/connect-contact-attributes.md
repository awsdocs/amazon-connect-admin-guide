# Use Amazon Connect Contact Attributes<a name="connect-contact-attributes"></a>

 In Amazon Connect, a contact is an interaction with a customer in your contact center\. The interaction can be a voice phone call with a human agent, or an automated interaction using an Amazon Lex bot\. Contact attributes in Amazon Connect refer to key\-value pairs that contain data about a contact\.

Using contact attributes, you can customize and personalize the experience customers have when they interact with your contact center\. Contact attributes let you store customer input or data about a customer, and then use it later in a contact flow\. You can also check the values of contact attributes and use a condition to determine the branching behavior of the contact flow based on the value\.

Contact attributes let you pass data between Amazon Connect and other services, such as Amazon Lex and AWS Lambda\. Contact attributes can be both set and consumed by each service\. For example, you could use a Lambda function to look up customer information, such as their name or order number, and use contact attributes to store the values returned to Amazon Connect\. You could then reference those attributes to include the customer's name in messages using text to speech, or store their order number so they do not have to enter it again\.

**Topics**
+ [Using Contact Attributes](#using-contact-attributes)
+ [Using Contact Attributes to Personalize the Customer Experience](#use-attributes-cust-exp)
+ [Use Amazon Connect Contact Attributes with Other Services](#attribs-external-references)
+ [Using Attributes in the Contact Control Panel](#use-attribs-ccp)
+ [Referencing Contact Attributes](#how-to-reference-attributes)
+ [Using System Metric Attributes](#attrib-system-metrics)
+ [System Attributes for Contact Flows](#system-attributes)
+ [Contact Attributes Available in Amazon Connect](#connect-attrib-list)
+ [System Metrics Attributes](#attribs-system-metrics-table)
+ [Media Streams Attributes](#media-stream-attribs)
+ [Telephony Call Metadata Attributes](#telephony-call-metadata-attributes)

## Using Contact Attributes<a name="using-contact-attributes"></a>

When you create a contact flow, you can create user\-defined contact attributes using **Set contact attributes** blocks\. You can then reference them in other parts of a contact flow using any other block that supports dynamic attributes\. For example, you could use a **Check contact attributes** block to compare the value of an attribute to a condition you define, and then route the contact based on the results of the comparison\. You could also retrieve data from external sources, and then create user\-defined attributes from the external data so that you can reference them later in a contact flow, such as the status of an order or an expected shipping date\.

Personalize the customer experience by including the customer's name when you use text to speech text in a **Play prompt** or **Get customer input** block to speak messages to your customer\. Use contact attributes to store input provided by a customer during an interaction with an Amazon Lex bot to enable automated interactions\.

As a best practice, make attributes and attribute values case\-sensitive, and always match case in each context where they are used\.

The following types of contact attributes are available in Amazon Connect:
+ **System**—Predefined attributes in Amazon Connect\. You can reference system attributes, but you cannot create them\. Some system attributes relate to contacts, and some relate to metrics\. Not all blocks in a contact flow support using System attributes\. For example, you cannot use a System attribute to store customer input\. Instead, use a user\-defined attribute to store the data input by a customer\.
+ **Agent**—A subset of system attributes related to agents in your contact center\.
+ **Queue metrics**—System metric attributes returned when you use a **Get queue metrics** block in your contact flow\.
+ **User\-defined**—Attributes that are created when a contact flow executes using **Set contact attributes** blocks\. When you get data from an external source, you can copy key\-value pairs as user\-defined attributes to reference later in a contact flow\. You can also create user\-defined attributes through the Amazon Connect API\.

  User\-defined attributes include all attributes set by using a **Set contact attributes** block in a contact flow\. User\-defined attributes are included in contact trace records \(CTRs\)\. They are available to Lambda functions that are invoked after the **Set contact attributes** block, and are created in the Attributes namespace\. They are also available to applications that integrate with the Contact Control Panel \(CCP\) for screenpop information, and can be referenced in contact flows\.
+ **External**—Attributes are created via a process external to Amazon Connect\. For example, when you use an **Invoke AWS Lambda function** block in a contact flow, or integrate with an Amazon Lex bot\.

  External attributes are returned as key\-value pairs from the most recent invocation of an **Invoke AWS Lambda function** block\. External attributes are overwritten with each invocation of the Lambda function\. You can access external attributes in contact flows via $\.External\.AttributeName\. For more information about using attributes in Lambda functions, see [Using AWS Lambda Functions with Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/connect-lambda-functions.html)\.

  These attributes are not included in CTRs, not passed to the next Lambda invocation, and not passed to the CCP for screenpop information\. However, they can be passed as Lambda function inputs on an **Invoke AWS Lambda function** block, or copied to user\-defined attributes via the **Set contact attributes** block\. When used in **Set contact attributes** blocks, the attributes that are copied are included in CTRs, and can be used in the CCP\.
+ **Lex slots**—External attribute for the slot name of an Amazon Lex bot\.
+ **Lex attributes**—Session attributes from an Amazon Lex bot interaction\.

## Using Contact Attributes to Personalize the Customer Experience<a name="use-attributes-cust-exp"></a>

Contact attributes in your contact flows can provide a more personalized customer experience\. For example, specify a custom flow based on comparing an attribute to a value\. You then route the contact based on the value comparison, such as routing customers to different tiers of support based on their account number\. Or retrieve a customer's name and save it as an attribute\. Include the name attribute in a text to speech string so that the customer's name is said during the interaction\.

The steps in the following sections describe how to use contact attributes with different blocks in a contact flow\.

### Using a Set Contact Attributes Block<a name="use-set-contact-attrib-block"></a>

Use a **Set contact attributes** block to set a value that is later referenced in a contact flow\. For example, create a personalized greeting for customers routed to a queue based on the type of customer account\. You could also define an attribute for a company name or line of business to include in the text to speech strings said to a customer\. The **Set contact attributes** block is useful for copying attributes retrieved from external sources to user\-defined attributes\.

**To set a contact attribute with a Set contact attributes block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Set contact attributes** block\.

1. Edit the **Set contact attributes** block, and choose **Use text**\.

1. For the **Destination key**, provide a name for the attribute, such as *Company*\. This is the value you use for the **Attribute** field when using or referencing attributes in other blocks\. For the **Value**, use your company name\.

   You can also choose to use an existing attribute as the basis for creating the new attribute\.

### Capture Customer Input and Store it as an Attribute<a name="capture-cust-input"></a>

You can use an attribute to request a callback number from a customer, store the value of the attribute, and then reference the attribute in a **Set callback number** block to set the number to dial the customer\. You could also use a **Store customer input** block to capture any numeric input from a customer, such as an account or order number\.

**To create an attribute from customer input with a Store customer input block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Store customer input** block\.

1. Edit the block, and select **Text to speech \(Ad hoc\)**\.

1. In the **Enter text** box, type a message that is said to customers when they call, such as “Please enter your phone number\.”

1. In the **Customer input** section, select **Phone number**, and then choose the format\. **Local format** is for a number in the same country as the region in which you created your Amazon Connect instance\. **International format/Enforce E\.164** is for numbers to a country other than the country in which you created your instance\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/connect-store-cust-input-phone.png)

1. Add a **Set callback number** block to your contact flow, and connect it to the **Get customer input** block\.

1. Under **Use attributes**, for **Type**, choose **System**\. For **Attribute**, choose **Stored customer input**\. The callback number is set to the number the customer entered when asked to enter their phone number\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/connect-set-callback-number-attrib.png)

### Using Attributes with a Lambda Function<a name="attribs-with-lambda"></a>

Retrieve data from a system your organization uses internally, such as an ordering system or other database with a Lambda function, and store the values as attributes that can then be referenced in a contact flow\.

When the Lambda function returns a response from your internal system, the response is key\-value pairs of data\. You can reference the values returned in the External namespace, for example $\.External\.attributeName\. To use the attributes later in a contact flow, you can copy the key\-value pairs to user\-defined attributes using a **Set contact attributes** block\. You can then define logic to branch your contact based on attribute values by using a **Check contact attributes** block\. Any contact attribute retrieved from a Lambda function is overwritten with the next invocation of a Lambda function\. Make sure you store external attributes if you want to reference them later in a contact flow\.

**To store an external value from a Lambda function as a contact attribute**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add an **Invoke AWS Lambda function** block, then choose the title of the block to open the settings for the block\.

1. Add the **Function ARN** to your AWS Lambda function that retrieves customer data from your internal system\.

1. After the **Invoke AWS Lambda function** block, add a **Set contact attributes** block and connect the **Success** branch of the **Invoke AWS Lambda function** block to it\.

1. Edit the **Set contact attributes** block, and select **Use attribute**\.

1. For **Destination key**, type a name to use as a reference to the attribute, such as customerName\. This is the value you use in the **Attribute** field in other blocks to reference this attribute\.

1. For the **Type**, choose **External**\.

1. For **Attribute** type the name of the attribute returned from the Lambda function\. The name of the attribute returned from the function will vary depending on your internal system and the function you use\.

After this block executes during a contact flow, the value is saved as a user\-defined attribute with the name specified by the **Destination key**, in this case customerName\. It can be accessed in any block that uses dynamic attributes\.

To branch your contact flow based on the value of an external attribute, such as an account number, use a **Check contact attributes** block, and then add a condition to compare the value of the attribute to\. Next, branch the contact flow based on the condition\.

****

1. In the **Check contact attributes** block, for **Attribute to check** do one of the following:
   + Select **External** for the **Type**, then enter the key name returned from the Lambda function in the **Attribute** field\.
**Important**  
Any attribute returned from an AWS Lambda function is overwritten with the next function invocation\. To reference them later in a contact flow, store them as user\-defined attributes\.
   + Select **User Defined** for the **Type**, and in the **Attribute** field, type the name that you specified as the **Destination key** in the **Set contact attributes** block\.

1. Choose **Add another condition**\.

1. Under **Conditions to check**, choose the operator for the condition, then enter a value to compare to the attribute value\. A branch is created for each comparison you enter, letting you route the contact based on the conditions specified\. If no condition is matched, the contact takes the **No Match** branch from the block\.

### "$" is a Special Character<a name="dollar-sign-special"></a>

Amazon Connect treats the "$" character as a special character\. You can't use it in a key when setting an attribute\. 

 For example, let's say you're creating an interact block with text\-to\-speech\. You set an attribute like this: 

 ` {"$one":"please read this text"} ` 

When Amazon Connect reads this text, it will read "dollar sign one" to the contact instead of "please read this text\." Also, if you were to include $ in a key and try to reference the value later using Amazon Connect, it won't retrieve the value\. 

Amazon Connect does log and pass the full key:value pair `({"_$one":"please read this text"})` to integrations such as Lambda\. 

## Use Amazon Connect Contact Attributes with Other Services<a name="attribs-external-references"></a>

You can reference contact attributes set in your Amazon Connect contact flow in other services, such as in an Amazon Lex bot or AWS Lambda function\. This allows data associated with the customer or the contact to be shared between services\. To use contact attributes to access other resources, set a user\-defined attribute in your contact flow and use the Amazon Resource Name \(ARN\) of the resource you want to access as the value for the attribute\. For example, to use an Amazon Connect prompt in a Lambda function, set a user\-defined attribute to the ARN for the prompt, and then access that attribute from the Lambda function\.

## Using Attributes in the Contact Control Panel<a name="use-attribs-ccp"></a>

Contact attributes also let you capture information and then present that information in a screenpop to an agent in the Contact Control Panel \(CCP\)\. Use contact attributes to customize the agent experience when using the CCP integrated with a customer relationship management \(CRM\) application\. Also use them when integrating Amazon Connect with a custom application using the Amazon Connect Streams API or Amazon Connect API\. You can use all user\-defined attributes, in addition to the customer number and the dialed number, in the CCP using the Amazon Connect Streams JavaScript library\. For more information, see [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams) or Amazon Connect API\.

When you use the Amazon Connect Streams API, you can access user\-defined attributes by invoking contact\.getAttributes\(\)\. You can access endpoints via contact\.getConnections\(\), where a connection has a getEndpoint\(\) invocation on it\.

To access the attribute directly from a Lambda function, use $\.External\.AttributeName\. If the attribute is stored to a user\-defined attribute from a **Set contact attributes** block, use $\.Attributes\.AttributeName\.

For example, included with your Amazon Connect instance, there is a contact flow named “Sample note for screenpop\.” In this contact flow, a **Set contact attributes** block is used to create an attribute from a text string\. The text, as an attribute, can be passed to the CCP to display a note to an agent\.

## Referencing Contact Attributes<a name="how-to-reference-attributes"></a>

The way you reference contact attributes depends on how they were created and how you are accessing them\. To reference attributes in the same namespace, such as a system attribute, you use the attribute name, or the name you specified as the **Destination key**\. To reference values in a different namespace, such as referencing an external attribute, you specify the JSONPath syntax to the attribute\.

For example, to reference a customer name from a Lambda function lookup, you use $\.External\.AttributeKey, replacing AttributeKey with the key \(or name\) of the attribute returned from the Lambda function\. To reference an attribute from an Amazon Lex bot, you use the format $\.Lex\. and then include the part of the Amazon Lex bot to reference, such as $\.Lex\.IntentName\. To reference the customer input to an Amazon Lex bot slot, use $\.Lex\.Slots\.*slotName*, replacing *slotName* with the name of the slot in the bot\.

To reference user\-defined attributes, such as those set with the **Set contact attributes** block, use the drop\-down menus in subsequent blocks to reference the attribute, or use the Attributes namespace in JSONPath to the attribute if used in a text field\. For example, if you create a user\-defined attribute in a **Set contact attributes** block, you reference it in one of the following ways:
+ In a block that supports attributes, such as a **Check contact attributes** block, choose **User Defined** for the **Type**, and use the value you entered for the **Destination key** in the **Attribute** field\.
+ In a text field in a block, such as a **Play prompt** block, use the JSONPath $\.Attributes\.DestinationKey, replacing DestinationKey with the value you entered in the **Destination key**\.

JSONPath is a standardized way to query elements of a JSON object\. JSONPath uses path expressions to navigate elements, nested elements, and arrays in a JSON document\. For more information about JSON, see [Introducing JSON](http://www.json.org/)\.

### Checking Attribute Values in a Check Contact Attributes Block<a name="check-contact-attrib-block"></a>

When you include a **Check contact attributes** block in a contact flow, it checks the value of the attribute you specify\. You then add a condition to compare the value of the attribute to, such as "greater than" or "contains\." For each condition you add, an output branch is added to the block\. You can then route the contact based on the conditions by connecting the output branch for the condition to the next block in the contact flow\. For example, you can check the current number of customers in a queue, then route the contact to the queue if the active contacts are fewer than 5\. You can also route the contact to another different queue if the number of active contacts is more than 5\. You can use whichever metrics or attributes you want to make routing decisions as appropriate for your needs\. The following procedure describes how to check for the number of contacts in a queue and then route the contact to a queue that has fewer than 5 active contacts in it\.

### Using a Check contact attributes block to route a contact to a queue

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

### Referencing Attributes from a Play Prompt Block<a name="attribs-play-prompt"></a>

Use a **Play prompt** block to use an audio file to play as a greeting or message to callers\. You can also use contact attributes to specify the greeting or message delivered to callers\. To use the values of a contact attribute to personalize a message for a customer, include references to stored or external contact attributes in the text\-to\-speech message\. For example, if you retrieved the customer’s name from a Lambda function, and it returns values from your customer database for FirstName and LastName, you could use these attributes to say the customer’s name in the text\-to\-speech block by including text similar to the following:

Hello $\.External\.FirstName $\.External\.LastName, thank you for calling\.

Alternatively, you could store the attributes returned from the Lambda function using a **Set contact attributes** block, and then reference the user\-defined attribute created in the text to speech string\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/connect-play-prompt-tts-attribs.png)

### Getting Customer Input Using an Amazon Lex Bot<a name="attribs-cust-input-lex-bot"></a>

When you reference attributes in a **Get customer input** block, and choose Amazon Lex as the method of collecting the input, the attribute values are retrieved and stored from the output from the customer interaction with the Amazon Lex bot\. You can use an attribute for each intent or slot used in the Amazon Lex bot, as well as the sessions attributes associated with the bot\. An output branch is added to the block for each intent you include\. When a customer chooses an intent when interacting with the bot, the branch associated with that intent is followed in the contact flow\.

### Using an Amazon Lex bot to get customer input

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

## Using System Metric Attributes<a name="attrib-system-metrics"></a>

Amazon Connect includes system metric attributes that can help you define routing conditions in your contact flows based on real\-time metrics about the queues and agents in your contact center\. When you include a **Get queue metrics** block in your contact flow, metrics are retrieved for the current working queue, or other queue that you specify, and returned as attributes that you can reference in blocks that occur after that block in the flow\.

You can reference the metric attributes returned to determine the optimal route for a contact\. Check the current queue metrics, such as the number of contacts or available agents in a queue, and how long the oldest contact has been in a queue\. You could even get metrics for multiple queues and use a **Set contact attributes** block to store the metric attributes for each queue\. You could then compare queue metric attributes using a **Check contact attributes** block, and route the contact to the queue with the fewest calls in it, or to a callback if all queues are busy\. To learn more about the metric attributes available, see [System Metrics Attributes](#attribs-system-metrics-table)\.

**To use system metrics attributes in a contact flow**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Get queue metrics** block to the contact flow\.

1. Optionally, to specify a queue select the **Set queue** check box and do one of the following:
   + Select the queue to retrieve metrics for from the drop\-down list\.
   + Select **Use attribute**, then select the attribute to use\.

   If you do not select a queue, metrics are retrieved for the current working queue\.

1. Add a **Check contact attributes** block and connect the **Success** branch of the **Get queue metrics** block to it\.

1. Choose the title of the **Check contact attributes** block to display the properties for the block\.

1. Under **Attribute to check**, in the **Type** drop\-down menu, choose **Queue metrics**\. In the **Attribute** drop\-down menu, select the attribute to check\. 

1. To create a branching condition based on the value of the metric attribute, choose **Add another condition**\.

1. For the **Conditions to check**, choose the conditions to compare the attribute value to, and then enter a value in the **Value** field\.

1. Add additional blocks to the contact flow, connecting the branch of the **Check contact attributes** block to route the contact to the next block in the flow\.

1. Save and publish the contact flow to make it available in your contact center\.

## System Attributes for Contact Flows<a name="system-attributes"></a>

When creating a contact flow, you can use the following system attributes in Amazon Connect:
+ **Customer number**—The phone number of the customer\. When used in an outbound whisper flow, this is the number the agents dialed to reach the customer\. When used in inbound flows, this is the number from which the customer placed the call\. This attribute is included in the CTRs and Lambda input object under CustomerEndpoint\.
+ **Dialed number**—The number that the customer dialed to reach your contact center\. This attribute is included in the CTRs and Lambda input under SystemEndpoint\.
+ **Customer callback number**—The number that the system uses to call the customer back, either for the **Transfer to callback** queue functionality, or for an agent dialing from the CCP\. The default value is the number the customer used to call your contact center, but can be overwritten with the **Set callback number** block\. This attribute is not included in CTRs, and not accessible in Lambda input\. You can copy the attribute to a user\-defined attribute with the **Set contact attribute** block, which is included in CTRs\. You can also pass this attribute as a Lambda input parameter in an **Invoke AWS Lambda function** block, which is not included in CTRs\.
+ **Stored customer input**—The attribute values created from the most recent **Store customer input** block invocation\. This attribute is not included in CTRs, and is not accessible in Lambda input\. You can copy the attribute to a user\-defined attribute with the **Set contact attribute** block, which is included in CTRs\. You can also pass this attribute as a Lambda input parameter in an **Invoke AWS Lambda function** block, which is not included in CTRs\. This attribute value applies only to the most recent invocation of the Lambda function\. It is overwritten with the next invocation of the function\.
+ **Queue name**—The name of the queue\.
+ **Queue ARN**—The ARN of the queue\.
+ **Queue outbound number**—The **Outbound caller ID number** selected for the queue\.
+ **Text to speech voice**—The Amazon Polly voice used for text to speech in a contact flow\.
+ **Contact id**—The unique identifier for the contact\.
+ **Initial contact id**—The unique identifier for the contact associated with the first interaction between the customer and your contact center\.
+ **Previous contact id**—The unique identifier for the leg of the contact that occurred before the current contact\.
+ **Channel**—The method used to contact your contact center\. Currently only VOICE is supported\.
+ **Instance ARN**—The ARN for your Amazon Connect instance\.
+ **Initiation method**—Indicates how the contact was initiated\. Valid values include: INBOUND, OUTBOUND, TRANSFER, CALLBACK, API, and QUEUE\_TRANSFER\.
+ **Lex intent**—The name of the intent as defined in your Amazon Lex bot\.

## Contact Attributes Available in Amazon Connect<a name="connect-attrib-list"></a>

The following sections describe the contact attributes available in Amazon Connect\.

### Contact Flow System Attributes<a name="attribs-system-table"></a>


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Customer number | The customer’s phone number\. | System | $\.CustomerEndpoint\.Address | 
| Dialed number | The number the customer dialed to call your contact center\. | System | $\.SystemEndpoint\.Address | 
| Customer callback number | The number to dial to call back the customer\. | System | not applicable | 
| Stored customer input | An attribute created from the most recent invocation of a **Store customer input ** block\. | System | not applicable | 
| Queue name | The name of the queue\. | System | $\.Queue\.Name | 
| Queue ARN | The ARN for the queue\. | System | $\.Queue\.ARN | 
| Text to speech voice | The name of the voice to use for text\-to\-speech\. | System | $\.TextToSpeechVoiceId | 
| Contact id | The unique identifier of the contact\. | System | $\.ContactId | 
| Initial contact id | The unique identifier for the first contact a customer had with your contact center\. Use the initial contact ID to track contacts between contact flows\.  | System | $\.InitialContactId | 
| Previous contact id | The unique identifier for the contact before it was transferred\. Use the previous contact ID to trace contacts between contact flows\. | System | $\.PreviousContactId | 
| Channel | The method of contact\. Currently, only VOICE is supported in Amazon Connect\. | System | $\.Channel | 
| Instance ARN | The ARN for your Amazon Connect instance\. | System | $\.InstanceARN | 
| Initiation method | How the contact was initiated\. Valid values include: INBOUND, OUTBOUND, TRANSFER, CALLBACK, and API\. | System | $\.InitiationMethod | 
| System Endpoint Type | The type of the system endpoint\. Valid value is TELEPHONE\_NUMBER\. | System | $\.SystemEndpoint\.Type | 
| Customer Endpoint type | The type of the customer endpoint\. Valid value is TELEPHONE\_NUMBER\. | System | $\.CustomerEndpoint\.Type | 
| Queue Outbound Caller ID number | The outbound caller ID number defined for the queue\. This can be useful for reverting the caller ID after setting a custom caller ID\. | System | $\.Queue\.OutboundCallerId\.Address | 
| Queue Outbound Caller ID number type | The type of the outbound caller ID number\. Valid value is TELEPHONE\_NUMBER\. | System | $\.Queue\.OutboundCallerId\.Type | 

### Agent Attributes<a name="attribs-agent"></a>

The following table lists the agent attributes available in Amazon Connect\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Agent User name | The user name an agent uses to log in to Amazon Connect\. | System | $\.Agent\.UserName | 
| Agent First name | The agent’s first name as entered in their Amazon Connect user account\.  | System | $\.Agent\.FirstName | 
| Agent Last name | The agent’s last name as entered in their Amazon Connect user account\. | System | $\.Agent\.LastName | 
| Agent ARN | The ARN of the agent\. | System | $\.Agent\.ARN | 

### Contact Attributes from Amazon Lex<a name="attribs-lex-table"></a>

The following table lists the attributes available from Amazon Lex bots\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Dialog state | The last dialog state returned from an Amazon Lex bot\. The value is 'Fulfilled' if an intent was returned to the contact flow\. | External | $\.Lex\.dialogState | 
| Intent name | The user intent returned by Amazon Lex\. | External | $\.Lex\.IntentName | 
| Slots | Map of intent slots \(key/value pairs\) Amazon Lex detected from the user input during the interaction\. | External | $\.Lex\.Slots\.slotName | 
| Session attributes | Map of key\-value pairs representing the session\-specific context information\. | External | $\.Lex\.sessionAttributes\.attributeKey | 

#### External Contact Attributes<a name="attribs-lambda-table"></a>

Attributes returned as key\-value pairs from a Lambda function are external attributes\. To reference external attributes in JSONPath, use $\.External\.attributeName, where AttributeName is the attribute name, or the key of the key\-value pair returned from the function\. For example, if the function returns a contact ID, reference the attribute with $\.External\.ContactId\. When referencing a contact ID returned from Amazon Connect, the JSONPath is $\.ContactId\. Note the inclusion of \.External in the JSONPath reference when the attribute is external to Amazon Connect\. Make sure to match the case for attribute names returned from external sources\.

## System Metrics Attributes<a name="attribs-system-metrics-table"></a>

The metrics attributes in the following table are returned when you use the **Get queue metrics** block to retrieve metrics for a queue\. If there is no current activity in your contact center, null values are returned for these attributes\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Queue name | The name of the queue for which metrics were retrieved\. | System | $\.Metrics\.Queue\.Name | 
| Queue ARN | The ARN of the queue for which metrics were retrieved\. | System | $\.Metrics\.Queue\.ARN | 
| Metrics queue size | The number of contacts currently in the queue\. | System | $\.Metrics\.Queue\.Size | 
| Oldest contact in queue | For the contact that has been in the queue the longest, the length of time that the contact has been in the queue, in seconds\. | System | $\.Metrics\.Queue\.OldestContactAge | 
| Agents online | The number of agents currently online, which means logged in and in any state other than offline\. | System | $\.Metrics\.Agents\.Online\.Count | 
| Agents available | The number of agents whose state is set to Available\. | System | $\.Metrics\.Agents\.Available\.Count | 
| Agents staffed | The number of agents currently staffed, which is agents logged in and in Available, ACW, or Busy states\. | System | $\.Metrics\.Agents\.Staffed\.Count | 
| Agents in After contact work | The number of agents currently in the ACW state\. | System | $\.Metrics\.Agents\.AfterContactWork\.Count | 
| Agents busy | The number of agents currently active on a contact\. | System | $\.Metrics\.Agents\.Busy\.Count | 
| Agents missed count | The number of agents in the Missed state, which is the state an agent enters after a missed contact\. | System | $\.Metrics\.Agents\.Missed\.Count | 
| Agents in non\-productive state | The number of agents in a non\-productive \(NPT\) state\. | System | $\.Metrics\.Agents\.NonProductive\.Count | 

## Media Streams Attributes<a name="media-stream-attribs"></a>

The following table lists the attributes you can use to identify the location in the live media stream where the customer audio starts and stops\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Customer audio stream ARN | The ARN of the Kinesis Video stream used for Live media streaming that includes the customer data to reference\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StreamARN | 
| Customer audio start timestamp in the Kinesis video stream used for Live media streaming\. | When the customer audio stream started\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StartTimestamp | 
| Customer audio stop timestamp | When the customer audio stream stopped the Kinesis video stream used for Live media streaming\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StopTimestamp | 
| Customer audio start fragment number | The number that identifies the Kinesis Video Streams fragment, in the stream used for Live media streaming, in which the customer audio stream started\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StartPosition | 

## Telephony Call Metadata Attributes<a name="telephony-call-metadata-attributes"></a>

Telephony metadata provides additional information from telephony carriers that identify the source of the end user before connecting to an agent\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| P\-Asserted\-Identity | The source of the end user\. | System | $\.Media\.Sip\.Headers\.P\-Asserted\-Identity | 
| P\-Charge\-Info | The party responsible for the charges associated with the call\. | System | $\.Media\.Sip\.Headers\.P\-Charge\-Info | 
| From | The identity of the end user associated with the request\. | System | $\.Media\.Sip\.Headers\.From | 
| To | Information about the called party or the recipient of the request\.  | System | $\.Media\.Sip\.Headers\.To | 

**Note**  
Telephony metadata is not consistent across all telephony providers\. In some cases, this may result in empty values\.