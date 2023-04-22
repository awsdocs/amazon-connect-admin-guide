# About mapping destinations<a name="about-mapping-destinations"></a>

A mapping destination is your mapping from a source to a standard definition that is already defined in Amazon Connect\.

The following table lists the supported mapping destinations\.


| Source object | Destination: Customer, Product, Order, Case | 
| --- | --- | 
|  S3  | Any  | 
|  Salesforce\-Account  | Customer  | 
|  Salesforce\-Contact  | Customer  | 
|  Salesforce\-Multi\-Contact\-Account\-Link  | Customer  | 
|  Salesforce\-Asset  | Product  | 
|  Salesforce\-Multi\-Asset\-Account\-Link  | Product  | 
|  Zendesk\-users  | Customer  | 
|  Marketo\-leads  | Customer  | 
|  Marketo\-Multi\-Lead\-Account\-Link  | Customer  | 
|  Servicenow\-sys\_user  | Customer  | 
|  Segment\-Identify  | Customer  | 
|  Segment\-Customer  | Customer  | 
|  Shopify\-Customer  | Customer  | 
|  Shopify\-DraftOrder  | Order  | 
|  Zendesk\-tickets  | Case  | 
|  Servicenow\-task  | Case  | 
|  Servicenow\-incident  | Case  | 

**Note**  
The following source objects resemble existing templates, but without **Account** as a profile identifier\. For more information on standard identifiers, see [Standard identifiers](standard-identifiers.md)\.  
**Salesforce\-Multi\-Asset\-Account\-Link**  
This source object allows you to ingest multiple assets that share a common **AccountID**\. In this case, we will create multiple profiles that can be retrieved via search based on their common **AccountID**\.
**Salesforce\-Multi\-Contact\-Account\-Link**  
This source object allows you to ingest multiple contacts that share a common **AccountID**\. In this case, we will create multiple profiles that can be retrieved via search based on their common **AccountID**\.
**Marketo\-Multi\-Lead\-Account\-Link**  
This source object allows you to ingest multiple leads that share a common **AccountID**\. In this case, we will create multiple profiles that can be retrieved via search based on their common **AccountID**\.