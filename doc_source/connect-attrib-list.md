# Contact Attributes Available in Amazon Connect<a name="connect-attrib-list"></a>

The following sections describe the contact attributes available in Amazon Connect\.

## Contact Flow System Attributes<a name="attribs-system-table"></a>


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
| Channel | The method of contact, either VOICE or CHAT\.  | System | $\.Channel | 
| Instance ARN | The ARN for your Amazon Connect instance\. | System | $\.InstanceARN | 
| Initiation method | How the contact was initiated\. Valid values include: INBOUND, OUTBOUND, TRANSFER, CALLBACK, and API\. | System | $\.InitiationMethod | 
| System Endpoint Type | The type of the system endpoint\. Valid value is TELEPHONE\_NUMBER\. | System | $\.SystemEndpoint\.Type | 
| Customer Endpoint type | The type of the customer endpoint\. Valid value is TELEPHONE\_NUMBER\. | System | $\.CustomerEndpoint\.Type | 
| Queue Outbound Caller ID number | The outbound caller ID number defined for the queue\. This can be useful for reverting the caller ID after setting a custom caller ID\. | System | $\.Queue\.OutboundCallerId\.Address | 
| Queue Outbound Caller ID number type | The type of the outbound caller ID number\. Valid value is TELEPHONE\_NUMBER\. | System | $\.Queue\.OutboundCallerId\.Type | 

## Agent Attributes<a name="attribs-agent"></a>

The following table lists the agent attributes available in Amazon Connect\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Agent User name | The user name an agent uses to log in to Amazon Connect\. | System | $\.Agent\.UserName | 
| Agent First name | The agent’s first name as entered in their Amazon Connect user account\.  | System | $\.Agent\.FirstName | 
| Agent Last name | The agent’s last name as entered in their Amazon Connect user account\. | System | $\.Agent\.LastName | 
| Agent ARN | The ARN of the agent\. | System | $\.Agent\.ARN | 

## Contact Attributes from Amazon Lex<a name="attribs-lex-table"></a>

The following table lists the attributes available from Amazon Lex bots\.


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| Dialog state | The last dialog state returned from an Amazon Lex bot\. The value is 'Fulfilled' if an intent was returned to the contact flow\. | External | $\.Lex\.dialogState | 
| Intent name | The user intent returned by Amazon Lex\. | External | $\.Lex\.IntentName | 
| Slots | Map of intent slots \(key/value pairs\) Amazon Lex detected from the user input during the interaction\. | External | $\.Lex\.Slots\.slotName | 
| Session attributes | Map of key\-value pairs representing the session\-specific context information\. | External | $\.Lex\.SessionAttributes\.attributeKey | 

### External Contact Attributes<a name="attribs-lambda-table"></a>

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

The following table lists the attributes that you can use to identify the location in the live media stream where the customer audio starts and stops\.


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