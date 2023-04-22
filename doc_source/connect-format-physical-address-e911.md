# Format a physical address for E911<a name="connect-format-physical-address-e911"></a>

This topic explains how to format a physical address so it can be passed to Amazon Connect\.

E911 outbound calls require a physical address to be passed to Amazon Connect as a JSON string with keys and values that represent the various fields in the address\. For example, consider the following US address:
+ 2121 7th Ave, Seattle, WA, 98121, USA

The address must be attached as a JSON string against the key `CivicAddress`, as shown in the following example\. Every address field is attached to a specific coded key\. 

 `CivicAddress: {"country":"USA","RD":"7th","A3":"Seattle","PC":"98121","HNO":"2121","STS":"Ave","A1":"WA"}`

The following illustration shows how an example input address maps to [PSAP](https://en.wikipedia.org/wiki/Public_safety_answering_point) address keys:

![\[The mapping of a physical address to PSAP address keys.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-example-mapping-scheme.png)

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

`return { ,'CivicAddress': json.dumps(json_agent_location) ,'agent_did_number': '+15555551212' }`

For an address such as the following example:
+ 2121 7th Ave, Seattle, WA, 98121, USA

The key\-value pair:

`CivicAddress: {"country": "USA", "RD": "7th", "A3": "Seattle", "PC": "98121", "HNO": "2121", "STS": "Ave", "A1": "WA"}`

And the corresponding JSON string that is actually passed to Amazon Connect:

`CivicAddress: {\"country\": \"USA\", \"RD\": \"7th\", \"A3"\: \"Seattle\", \"PC\": \"98121\", \"HNO\": \"2121\", \"STS\": \"Ave\", \"A1\": \"WA\"}`

**Note**  
Using `json.dumps` adds an escape character **\\** to each quotation mark \(**"**\)\.