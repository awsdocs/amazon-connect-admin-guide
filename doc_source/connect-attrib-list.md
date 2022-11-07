# List of available contact attributes and their JSONPath reference<a name="connect-attrib-list"></a>

The following tables describe the contact attributes available in Amazon Connect\.

The JSONPath reference for each attribute is provided so you can [create dynamic text strings](create-dynamic-text-strings.md)\. 

## System attributes<a name="attribs-system-table"></a>

These are predefined attributes in Amazon Connect\. You can reference system attributes, but you cannot create them\. 

Not all blocks in a flow support using System attributes\. For example, you cannot use a System attribute to store customer input\. Instead, use a [ user\-defined attribute](#user-defined-attributes) to store the data input by a customer\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Customer number | The customer's phone number\. When used in an outbound whisper flow, this is the number that the agents dialed to reach the customer\. When used in inbound flows, this is the number from which the customer placed the call\. This attribute is included in contact records\. When used in a Lambda function, it's included in the input object under CustomerEndpoint\.  | System | $\.CustomerEndpoint\.Address | 
| Customer ID | The customer's identification number\.  | System | $\.CustomerId | 
| Dialed number | The number the customer dialed to call your contact center\. This attribute is included in contact records\. When used in a Lambda function, it's included in the input object under SystemEndpoint\. | System | $\.SystemEndpoint\.Address | 
| Customer callback number | The number that Amazon Connect uses to call back the customer\. This number can be the one used for a queued callback, or when an agent is dialing from the CCP\. Transfer to callback queue functionality, or for an agent dialing from the CCP\. The default value is the number that the customer used to call your contact center\. However, it can be overwritten with the **Set callback number** block\.  This attribute is not included in contact records, and it's not accessible in Lambda input\. However, you can copy the attribute to a user\-defined attribute with the Set contact attribute block, which is included in contact records\. You can also pass this attribute as a Lambda input parameter in an Invoke AWS Lambda function block, which is not included in contact records\.  | System | not applicable | 
| Stored customer input | An attribute created from the most recent invocation of a **Store customer input** block\. The attribute values created from the most recent Store customer input block invocation\. This attribute is not included in contact records, and is not accessible in Lambda input\. You can copy the attribute to a user\-defined attribute with the Set contact attribute block, which is included in contact records\. You can also pass this attribute as a Lambda input parameter in an Invoke AWS Lambda function block,  | System | not applicable | 
| Queue name | The name of the queue\. | System | $\.Queue\.Name | 
| Queue ARN | The ARN for the queue\. | System | $\.Queue\.ARN | 
| Queue outbound number | The Outbound caller ID number for the selected queue\. This attribute is only available in outbound whisper flows\. | System |  | 
| Text to speech voice | The name of the Amazon Polly voice to use for text\-to\-speech in a contact flow\. | System | $\.TextToSpeechVoiceId | 
| Contact id | The unique identifier of the contact\. | System | $\.ContactId | 
| Initial Contact id | The unique identifier for the contact associated with the first interaction between the customer and your contact center\. Use the initial contact ID to track contacts between flows\.  | System | $\.InitialContactId | 
| Task Contact id | The unique identifier for the task contact\. Use the task contact ID to track tasks between flows\.  | System | $\.Task\.ContactId | 
| Previous Contact id | The unique identifier for the contact before it was transferred\. Use the previous contact ID to trace contacts between flows\. | System | $\.PreviousContactId | 
| Channel | The method used to contact your contact center: VOICE, CHAT, TASK\.   | System | $\.Channel | 
| Instance ARN | The ARN for your Amazon Connect instance\. | System | $\.InstanceARN | 
| Initiation method | How the contact was initiated\. Valid values include: INBOUND, OUTBOUND, TRANSFER, CALLBACK, QUEUE\_TRANSFER, DISCONNECT, and API\. Initiation method doesn't work in Agent whisper flows or Customer whisper flows\. | System | $\.InitiationMethod | 
| Name | The name of the task\. | System | $\.Name | 
| Description | A description of the task\. | System | $\.Description | 
| References | Links to other documents that are related to a contact\. | System | $\.References\.*ReferenceKey*\.Value and $\.References\.*ReferenceKey*\.Type where *ReferenceKey* is the user\-defined Reference name\. | 
| Language | The language of content\. Use the standard java\.util\.Locale\. For example, en\-US for United States English, jp\-JP for Japanese, etc\. | System | $\.LanguageCode | 
| System Endpoint Type | The type of the system endpoint\. Valid value is TELEPHONE\_NUMBER\. | System | $\.SystemEndpoint\.Type | 
| Customer Endpoint type | The type of the customer endpoint\. Valid value is TELEPHONE\_NUMBER\. | System | $\.CustomerEndpoint\.Type | 
| Queue Outbound Caller ID number | The outbound caller ID number defined for the queue\. This can be useful for reverting the caller ID after setting a custom caller ID\. | System | $\.Queue\.OutboundCallerId\.Address | 
| Queue Outbound Caller ID number type | The type of the outbound caller ID number\. Valid value is TELEPHONE\_NUMBER\. | System | $\.Queue\.OutboundCallerId\.Type | 

## Agent attributes<a name="attribs-agent"></a>

The following table lists the agent attributes available in Amazon Connect\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Agent User name | The user name an agent uses to log in to Amazon Connect\. | System | $\.Agent\.UserName | 
| Agent First name | The agent’s first name as entered in their Amazon Connect user account\.  | System | $\.Agent\.FirstName | 
| Agent Last name | The agent’s last name as entered in their Amazon Connect user account\. | System | $\.Agent\.LastName | 
| Agent ARN | The ARN of the agent\. | System | $\.Agent\.ARN | 

**Note**  
When you use an agent contact attribute in a **Transfer to agent** flow, the agent attributes reflect the target agent, not the one who initiated the transfer\.

Agent attributes are available only in the following types of flows:
+ Agent whisper
+ Customer whisper
+ Agent hold
+ Customer whisper
+ Outbound whisper
+ Transfer to agent\. In this case, the agent attributes reflect the target agent, not the one who initiated the transfer\.

Agent attributes are not available in the following flow types:
+ Customer queue
+ Transfer to queue
+ Inbound flow

## Queue attributes<a name="attribs-system-metrics-table"></a>

These system attributes are returned when you use a **Get queue metrics** block in your flow\.

If there is no current activity in your contact center, null values are returned for these attributes\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Queue name | The name of the queue for which metrics were retrieved\. | System | $\.Metrics\.Queue\.Name | 
| Queue ARN | The ARN of the queue for which metrics were retrieved\. | System | $\.Metrics\.Queue\.ARN | 
| Contacts in queue | The number of contacts currently in the queue\. | System | $\.Metrics\.Queue\.Size | 
| Oldest contact in queue | For the contact that has been in the queue the longest, the length of time that the contact has been in the queue, in seconds\. | System | $\.Metrics\.Queue\.OldestContactAge | 
| Agents online | The number of agents currently online, which means logged in and in any state other than offline\. | System | $\.Metrics\.Agents\.Online\.Count | 
| Agents available | The number of agents whose state is set to Available\. | System | $\.Metrics\.Agents\.Available\.Count | 
| Agents staffed | The number of agents currently staffed, which is agents logged in and in Available, ACW, or Busy states\. | System | $\.Metrics\.Agents\.Staffed\.Count | 
| Agents in After contact work | The number of agents currently in the ACW state\. | System | $\.Metrics\.Agents\.AfterContactWork\.Count | 
| Agents busy | The number of agents currently active on a contact\. | System | $\.Metrics\.Agents\.Busy\.Count | 
| Agents missed count | The number of agents in the Missed state, which is the state an agent enters after a missed contact\. | System | $\.Metrics\.Agents\.Missed\.Count | 
| Agents in non\-productive state | The number of agents in a non\-productive \(NPT\) state\. | System | $\.Metrics\.Agents\.NonProductive\.Count | 

## Telephony call metadata attributes \(call attributes\)<a name="telephony-call-metadata-attributes"></a>

Telephony metadata provides additional information related to call origination from telephony carriers\. 


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| P\-Asserted\-Identity | The source of the end user\. | System | $\.Media\.Sip\.Headers\.P\-Asserted\-Identity | 
| P\-Charge\-Info | The party responsible for the charges associated with the call\. | System | $\.Media\.Sip\.Headers\.P\-Charge\-Info | 
| From | The identity of the end user associated with the request\. | System | $\.Media\.Sip\.Headers\.From | 
| To | Information about the called party or the recipient of the request\.  | System | $\.Media\.Sip\.Headers\.To | 
| ISUP\-OLI | Originating Line Indicator \(OLI\)\. Shows the type of line placing call \(for example, PSTN, 800 service call, wireless/cellular PCS, payphone\)\. | System | $\.Media\.Sip\.Headers\.ISUP\-OLI | 
| JIP | Jurisdiction Indication Parameter \(JIP\)\. Indicates geographic location of caller/switch\.  Example value: 212555 | System | $\.Media\.Sip\.Headers\.JIP | 
| Hop\-Counter | Hop Counter\.  Example value: 0  | System | $\.Media\.Sip\.Headers\.Hop\-Counter | 
| Originating\-Switch | Originating Switch\.  Example value: 710   | System | $\.Media\.Sip\.Headers\.Originating\-Switch | 
| Originating\-Trunk | Originating Trunk\. Example value: 0235 | System | $\.Media\.Sip\.Headers\.Originating\-Trunk | 
| Call\-Forwarding\-Indicator | Call Forwarding Indicators \(for example, Diversion header\)\. Indicates domestic or international origin of call\.  Example value: sip:\+15555555555@public\-vip\.us2\.telphony\-provider\.com;reason=unconditional  | System | $\.Media\.Sip\.Headers\.Call\-Forwarding\-Indicator | 
| Calling\-Party\-Address | Calling Party Address \(number\)\. NPAC dip shows true line type and native geographic switch\. Example value: 15555555555;noa=4  | System | $\.Media\.Sip\.Headers\.Calling\-Party\-Address | 
| Called\-Party\-Address | Called Party Address \(number\)\.  Example value: 15555555555;noa=4   | System | $\.Media\.Sip\.Headers\.Called\-Party\-Address | 

**Note**  
The availability of telephony metadata is not consistent across all telephony providers and may not be available in all cases\. This may result in empty values\. 

## Media streams attributes<a name="media-stream-attribs"></a>

The following table lists the attributes that you can use to identify the location in the live media stream where the customer audio starts and stops\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Customer audio stream ARN | The ARN of the Kinesis Video stream used for Live media streaming that includes the customer data to reference\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StreamARN | 
| Customer audio start timestamp in the Kinesis video stream used for Live media streaming\. | When the customer audio stream started\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StartTimestamp | 
| Customer audio stop timestamp | When the customer audio stream stopped the Kinesis video stream used for Live media streaming\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StopTimestamp | 
| Customer audio start fragment number | The number that identifies the Kinesis Video Streams fragment, in the stream used for Live media streaming, in which the customer audio stream started\. | Media streams | $\.MediaStreams\.Customer\.Audio\.StartFragmentNumber | 

## Amazon Lex contact attributes<a name="attribs-lex-table"></a>

The following table lists the attributes that are returned from Amazon Lex bots\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Alternate Intents | List of alternate intents available from Amazon Lex\. Each intent has a corresponding confidence score and slots to fill\. | Lex | $\.Lex\.AlternateIntents\.x\.IntentName $\.Lex\.AlternateIntents\.x\.IntentConfidence $\.Lex\.AlternateIntents\.x\.Slots $\.Lex\.AlternateIntents\.y\.IntentName $\.Lex\.AlternateIntents\.y\.IntentConfidence $\.Lex\.AlternateIntents\.y\.Slots $\.Lex\.AlternateIntents\.z\.IntentName $\.Lex\.AlternateIntents\.z\.IntentConfidence  $\.Lex\.AlternateIntents\.z\.Slots  | 
| Intent Confidence Score | The intent confidence score returned by Amazon Lex\. | Lex | $\.Lex\.IntentConfidence\.Score | 
| Intent name | The user intent returned by Amazon Lex\. | Lex | $\.Lex\.IntentName | 
| Sentiment Label |  The inferred sentiment that Amazon Comprehend has the highest confidence in\.   | Lex | $\.Lex\.SentimentResponse\.Label  | 
| Sentiment scores |  The likelihood that the sentiment was correctly inferred\.   | Lex | $\.Lex\.SentimentResponse\.Scores\.Positive $\.Lex\.SentimentResponse\.Scores\.Negative $\.Lex\.SentimentResponse\.Scores\.Mixed $\.Lex\.SentimentResponse\.Scores\.Neutral | 
| Session attributes |   Map of key\-value pairs representing the session\-specific context information\.   | Lex | $\.Lex\.SessionAttributes\.attributeKey | 
| Slots | Map of intent slots \(key/value pairs\) Amazon Lex detected from the user input during the interaction\.   | Lex | $\.Lex\.Slots\.slotName | 
| Dialog state | The last dialog state returned from an Amazon Lex bot\. The value is 'Fulfilled' if an intent was returned to the flow\. | N/A \(no type appears in the UI\) | $\.Lex\.DialogState | 

## Case contact attributes<a name="attribs-case-table"></a>

The following table lists the attributes that are used with Amazon Connect Cases\.


| Attribute | Description | Type | JSONPath Reference | Where the data comes from | 
| --- | --- | --- | --- | --- | 
|  Case ID  | Unique Identifier of the case in UUID format \(for example, 689b0bea\-aa29\-4340\-896d\-4ca3ce9b6226\) | text |  $\.Case\.case\_id  | Amazon Connect | 
|  Case Reason  | The reason for opening the case |  single\-select  | $\.Case\.case\_reason | Agent | 
|  Customer  | The API is a customer profile ID\. On the Cases: Fields page, the customer's name is displayed\. |  text  | $\.Case\.customer\_id | Amazon Connect | 
|  Date/Time Closed  | The date and time the case was last closed\. It does not guarantee that a case is closed\. If a case is reopened, this field contains the date/time stamp of the last time the status was changed to closed\. |  date\-time  | $\.Case\.last\_closed\_datetime  | Amazon Connect | 
|  Date/Time Opened  | The date and time the case was opened\. |  date\-time  | $\.Case\.created\_datetime | Amazon Connect | 
|  Date/Time Updated  | The date and time the case was last updated\. |  date\-time   | $\.Case\.last\_updated\_datetime | Amazon Connect | 
|  Reference number  | A friendly number for the case in 8\-digit numeric format\. Reference numbers \(unlike the Case ID\) are not guaranteed to be unique\. We recommend that you identify the customer and then collect the reference number to correctly find the right case\.  |  text  | $\.Case\.reference\_number | Agent | 
|  Status  | Current status of the case  |  text  | $\.Case\.status | Agent | 
|  Summary  | Summary of the case  |  text  | $\.Case\.summary | Agent | 
|  Title  | Title of the case  |  text  | $\.Case\.title | Agent | 

## Lambda contact attributes<a name="attribs-lambda-table"></a>

Lambda attributes are returned as key\-value pairs from the most recent invocation of an **Invoke AWS Lambda function** block\. External attributes are overwritten with each invocation of the Lambda function\.

To reference external attributes in JSONPath, use:
+ `$.External.attributeName`

where `AttributeName` is the attribute name, or the key of the key\-value pair returned from the function\. 

For example, if the function returns a contact ID, reference the attribute with ` $.External.ContactId`\. When referencing a contact ID returned from Amazon Connect, the JSONPath is `$.ContactId`\. 

**Note**  
Note the inclusion of `.External` in the JSONPath reference when the attribute is external to Amazon Connect\. Make sure to match the case for attribute names returned from external sources\.

For more information about using attributes in Lambda functions, see [Invoke AWS Lambda functions](connect-lambda-functions.md)\.

These attributes are not included in contact records, not passed to the next Lambda invocation, and not passed to the CCP for screenpop information\. However, they can be passed as Lambda function inputs on an **Invoke AWS Lambda function** block, or copied to user\-defined attributes via the **Set contact attributes** block\. When used in **Set contact attributes** blocks, the attributes that are copied are included in contact records, and can be used in the CCP\.

## User\-defined attributes<a name="user-defined-attributes"></a>

For all other attributes Amazon Connect defines the key and value\. For user\-defined attributes, however, you provide a name for the key and the value\.

Use user\-defined attributes in situations where you want to store values in a contact flow, and then refer to those values later\. For example, if you integrate Amazon Connect and a CRM or other system, you might want to get input from the customer such as their member number\. Then you can use that member number retrieve information about the member from the CRM, and/or use the member number throughout the flow, etc\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Any name you choose | A user\-defined attribute has two parts: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/connect-attrib-list.html)  | User\-defined | $\.Attributes\.*name\_of\_your\_destination\_key* | 

To create user\-defined attributes, use the [Set contact attributes](set-contact-attributes.md) block\. 

## Apple Messages for Business attributes<a name="apple-business-chat-attributes"></a>

Use the following contact attributes to route Apple Business Chat customers\. For example, if you have different lines of business using Apple Business Chat, you can branch to different flows based on the AppleBusinessChatGroup contact attribute\. Or, if you want to route Apple Business Chat messages differently from other chat messages, you can branch based on MessagingPlatform\. 


| Attribute | Description | Type | JSON | 
| --- | --- | --- | --- | 
|  MessagingPlatform  |  The messaging platform from where the customer request originated\.  Exact value: **AppleBusinessChat**  | User\-defined | $\.Attributes\.MessagingPlatform | 
|  AppleBusinessChatCustomerId  |  The customer’s opaque ID provided by Apple\. This remains constant for the AppleID and a business\. You can use this to identify if the message is from a new customer or a returning customer\.  | User\-defined | $\.Attributes\.AppleBusinessChatCustomerId | 
|  AppleBusinessChatIntent  |  You can define the intent or purpose of the chat\. This parameter is included in a URL that initiates a chat session in Messages when a customer chooses the **Business Chat** button\.  | User\-defined | $\.Attributes\.AppleBusinessChatIntent | 
|  AppleBusinessChatGroup  |  You define the group which designates the department or individuals best qualified to handle the customer’s particular question or problem\. This parameter is included in a URL that initiates a chat session in Messages when a customer chooses the **Business Chat** button\.   | User\-defined | $\.Attributes\.AppleBusinessChatGroup | 
|  AppleBusinessChatLocale  |  Defines the language and AWS Region preferences that the user wants to see in their user interface\. It consists of a language identifier \(ISO 639\-1\) and a Region identifier \(ISO 3166\)\. For example, **en\_US**\.   | User\-defined | $\.Attributes\.AppleBusinessChatLocale | 

## Customer Profiles attributes<a name="customer-profiles-attributes"></a>

Use the following contact attributes to autopopulate customer profiles in the agent app using the value of your choosing\. 


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| profileSearchKey | A user\-defined attribute that has two parts: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/connect-attrib-list.html)  | User\-defined | $\.Attributes\.*name\_of\_your\_destination\_key* | 