# Provision E911 in Amazon Connect<a name="implement-e911-flow"></a>

This topic explains how to provision E911 in Amazon Connect\.

## Detect a 911 call in Amazon Connect<a name="connect-detect-911-dial"></a>

For outbound voice calls within Amazon Connect, an [Outbound whisper flow](create-contact-flow.md#contact-flow-types) specifies the whisper to be played to customer\. You can configure an [Outbound whisper flow](create-contact-flow.md#contact-flow-types) to do the following:

1. Inspect the outbound call string from an agent\. 

1. If the string equals **911** \(or **933** in a test environment\), then retrieve the stored location/physical address for that agent by using a Lambda function\.

1. Attach the physical address to a contact attribute and proceed with the 911 \(or 933\) outbound call\. 

The following image shows an example [Outbound whisper flow](create-contact-flow.md#contact-flow-types)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-example-outbound-whisper.png)
+ Step 1: Call a Lambda function that retrieves the location for an agent \(Input parameter = Agent User Name\)\. The following image shows how to configure a [Invoke AWS Lambda function](invoke-lambda-function-block.md) block is so the agent **username** is passed to the Lambda function\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-invoke-lambda-block.png)
+ Step 2: Attach the location received to a contact attribute \(see [Format a physical address for E911](#connect-format-physical-address-e911) for the required format\)\.
+ Step 3: Update the call origination to the agent's phone number and continue with the outbound call\. 
**Note**  
The origination number is the caller ID that is passed along with the 911 outbound call\. If the origination phone number supports inbound calls, emergency responders will be able to call back the agent in case the initial phone call was disconnected\.  
The 911 call is specific to United States\. As a result, the origination phone number must be a valid US phone number\.   
For example, when an agent places an outbound call, if an invalid US phone number is passed to the carrier network, the carrier can reject the call\. To avoid this situation, if the agent uses an invalid number from Amazon Connect, Amazon Connect defaults to the Caller ID that is assigned to the queue in the agent's routing profile\.
The capability does not place any other rules on this number\. For example, the origination number can the phone number of the security front desk\.

## Format a physical address for E911<a name="connect-format-physical-address-e911"></a>

E911 outbound calls require a physical address to be passed to Amazon Connect as a JSON string with keys and values that represent the various fields in the address\. For example, consider the following US address:
+ 2121 7th Ave, Seattle, WA, 98121, USA

The address must be attached as a JSON string against the key `CivicAddress`, as shown in the following example\. Every address field is attached to a specific coded key\. 

 `CivicAddress: {"country":"USA","RD":"7th","A3":"Seattle","PC":"98121","HNO":"2121","STS":"Ave","A1":"WA"}`

The following table shows a complete list of keys\.


| Attribute name | Description | Example | Required | Character limit | Recommended character limit | 
| --- | --- | --- | --- | --- | --- | 
|  country  | The country is identified by the two\-letter ISO 3166 code\.  | US  | Required  | 2  |   | 
|  A1  | National subdivisions \(state, region, province, prefecture\)  | NY  | Required  | 2  |   | 
|  A3  | City, township, shi \(JP\)  | New York  | Required  | 32  |   | 
|  PRD  | Leading street direction  | N, W  | Required only if applicable to address  | 2  |   | 
|  POD  | Trailing street suffix  | SW  | Required only if applicable to address  | 2  |   | 
|  STS  | Street suffix  | Avenue, Platz  | Required only if applicable to address  | 5  |   | 
|  HNO  | House number \(numeric part only\)  | 2121  | Required  | 10  |   | 
|  HNS  | House number suffix  | A, 1/2  | Required only if applicable to address  | 4  |   | 
|  LOC  | Additional location information  | Room 543  | Optional  | 60  | 20 or less  | 
|  NAM  | Name \(residence, business or office occupant\)  | Example Corp  | Optional  | 32  |   | 
|  PC  | Postal code  | 10027  | Required  | 5  |   | 
|  RD  | Primary road or street  | Broadway  | Required  | 40  |   | 

**Note**  
It is your responsibility to validate the address against a standard repository such as the Master Street Address Guide \(MSAG\)\.

## Programming notes<a name="connect-e911-programming-notes"></a>

Currently it isn't possible to pass a JSON structure as an `Attribute` to Amazon Connect\. Therefore, the location retrieved by the Lambda function needs to be converted to a JSON string before it is passed to Amazon Connect\. For example, using the Python programming language, if the location retrieved is stored in a JSON structure `json_agent_location` then it can be passed to Amazon Connect \(from the Lambda function\) as follows:

` return { ,'CivicAddress': json.dumps(json_agent_location) ,'agent_did_number': '+15555551212' }`

For an address such as the following example:
+ 2121 7th Ave, Seattle, WA, 98121, USA

The key\-value pair:

`CivicAddress: {"country": "USA", "RD": "7th", "A3": "Seattle", "PC": "98121", "HNO": "2121", "STS": "Ave", "A1": "WA"}`

And the corresponding JSON string that is actually passed to Amazon Connect:

`CivicAddress: {\"country\": \"USA\", \"RD\": \"7th\", \"A3"\: \"Seattle\", \"PC\": \"98121\", \"HNO\": \"2121\", \"STS\": \"Ave\", \"A1\": \"WA\"}`

**Note**  
Using `json.dumps` adds an escape character **\\** to each quotation mark \(**"**\)\.

## Set up notifications when an E911 call is placed<a name="connect-e911-notifications"></a>

For 911 it is important to notify the corporate security or HR administrator to be notified in real time that someone from the contact center has placed an E911 call\. To do this, create an Amazon Connect task in the [Outbound whisper flow](create-contact-flow.md#contact-flow-types)\. Then add custom notification logic to the task\. 

The following image shows an example of a [Create task](create-task-block.md) block in an [Outbound whisper flow](create-contact-flow.md#contact-flow-types)\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-create-task-flow.png)

The following image shows an example of how to configure the [Create task](create-task-block.md) block for this use case\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-create-task-config.png)