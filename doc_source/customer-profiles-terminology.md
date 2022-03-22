# Concepts and terminology for customer object type mappings<a name="customer-profiles-terminology"></a>

The following terminology and concepts are central to your understanding of custom object type mappings\. 

**Standard profile object**  <a name="StandardProfileObject"></a>
A *standard profile object* is a predefined object that all profiles contain\.   
A standard profile object contains standard fields, such as phone numbers, email addresses, name and other standard data\. This data can be retrieved in a standard format regardless of the source \(for example, Salesforce, ServiceNow, or Marketo\)\.

**Profile object**  <a name="ProfileObject"></a>
A *profile object* is a single unit of information known about a profile\. For example, the information about a phone call, a ticket, a case, or even a click\-stream record from a web site\.  
A single profile object can be up to 250 KB and can be any structured JSON document\.   
+ Every profile object has a type\. For example, the profile object can be an Amazon Connect contact record, ServiceNow Users, or Marketo Leads\. 
+ The type refers to the object type mapping\.
+ The object type mapping defines how that specific object should be ingested into Customer Profiles\.

**Profile**  <a name="Profile"></a>
A *profile* contains all the information known about a specific customer or contact\. It includes a single standard profile object and any number of additional profile objects\.

**Object type mapping**  <a name="ObjectTypeMapping"></a>
The *object type mapping* tells Customer Profiles how to ingest a specific type of data\. It provides Customer Profiles with the following information:   
+ How data should be populated from the object and ingested into the standard profile object\. 
+ What fields should be indexed in the object and how those fields should then be used to assign objects of this type to a specific profile\.

**Mapping template**  <a name="MappingTemplate"></a>
A *mapping template* is a predefined object type mapping included with the Customer Profiles service\.  
Customer Profiles includes mapping templates for Amazon Connect contact records, Salesforce Accounts, ServiceNow Users, and Marketo Leads\. For a complete list of available mapping templates, use the [ListProfileObjectTypeTemplates](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjectTypeTemplates.html) API\.  
With mapping templates you can quickly ingest data from well known sources without having to specify any additional information\.