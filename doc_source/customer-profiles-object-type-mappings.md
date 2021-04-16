# Create and ingest customer data into Customer Profiles by using Amazon S3<a name="customer-profiles-object-type-mappings"></a>

You can define data from any source using Amazon S3 and seamlessly enrich a customer profile without the need for custom or pre\-built integrations\. For example, say you want to provide agents with relevant purchase history information\. You can import purchase transaction data from an internal application into a spreadsheet file on S3 and then link it to a customer profile\.

To set this up, you need to define an object type mapping that describes what the custom profile object looks like\. This mapping defines how fields from your data can be used to either populate fields in the standard profile or how it can be used to assign the data to a specific profile\. 

After you create the object type mapping, you can use the [PutProfileObject ](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutProfileObject .html) API to upload the custom profile data from your CRM into the custom profile object\. 

This topic explains how to create a mapping for your custom profile objects\.

## Concepts<a name="customer-profiles-terminology"></a>

The following terminology and concepts are central to your understanding of custom object type mappings\. 

**Standard profile object**  <a name="StandardProfileObject"></a>
A *standard profile object* is a predefined object that all profiles contain\.   
A standard profile object contains standard fields, such as phone numbers, email addresses, name and other standard data\. This data can be retrieved in a standard format regardless of the source \(for example, Salesforce, ServiceNow, or Marketo\)\.

**Profile object**  <a name="ProfileObject"></a>
A *profile object* is a single unit of information known about a profile\. For example, the information about a phone call, a ticket, a case, or even a click\-stream record from a web site\.  
A single profile object can be up to 250 KB and can be any structured JSON document\.   
+ Every profile object has a type\. For example, the profile object can be Amazon Connect Contact Trace Record \(CTR\), ServiceNow Users, or Marketo Leads\. 
+ The type refers to the object type mapping\.
+ The object type mapping defines how that specific object should be ingested into Customer Profiles\.

**Profile**  <a name="Profile"></a>
A *profile* contains all the information known about a specific customer or contact\. It includes a single standard profile object and any number of additional profile objects\.

**Object type mapping**  <a name="ObjectTypeMapping"></a>
The *object type mapping* tells Customer Profiles how to ingest a specific type of data\. It provides Customer Profiles with the following information:   
+ How data should be populated from the object and ingested into the standard profile object\. 
+ What fields should be indexed in the object and how those fields should then be used to assign objects of this type to a specific profile\.

**Mapping template**  <a name="MappingTemplate"></a>
A *mapping template* is a predefined object type mapping included with the Customer Profile service\.  
Customer Profiles includes mapping templates for Amazon Connect Contact Trace Records \(CTRs\), Salesforce Accounts, ServiceNow Users, and Marketo Leads\. For a complete list of available mapping templates, use the [ListProfileObjectTypeTemplates](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjectTypeTemplates.html) API\.  
With mapping templates you can quickly ingest data from well known sources without having to specify any additional information\.

## Object type mapping requirements<a name="object-type-mapping-requirements"></a>

The following information needs to be in your object type mapping so Customer Profiles can process the incoming data: 
+ A definition of all the fields in the ingested object that should be mapped to the standard profile, or used for assigning the data to a profile\. This tells Customer Profiles which fields in the ingested **source** object should be mapped to given fields in the standard profile object\.
+ Which fields in the source object from your custom data should be indexed and how\. 

  When the source data is ingested by Customer Profiles, the indexed fields determine:
  + Which profile a specific object belongs to\.
  + Which objects are related to each other and should be placed in the same profile\. For example, an account number or a CTR contact ID\. 
  + What values can be used to find a profile\. For example, the contact's name can be indexed\. This would allow agents to find all profiles that belong to customers with a specific name\. 

### Key requirements<a name="key-requirements"></a>

You must define at least one key\. Customer Profiles uses this key to map your custom profile object to a profile\.

The custom profile object mapping also needs at least one key that uniquely identifies the object so that it can be updated by specifying the same value of this field \(these requirements can be satisfied with a single key\)\.

Each key can be made up of one or more fields\. 

### Field requirements<a name="field-requirements"></a>

A field definition specifies how to read a value for that field name from a source object\. The field definition also specifies what kind of data is stored in the field\.

Object type names can be any alpha numerical string or the '\-' and '\_' character, they also cannot start with a '\_' character, which is used for reserved standard object types\.

## Object type mapping definition details<a name="object-type-mapping-definition-details"></a>

The object type mapping definition has two parts: the field definition and the key definition\. 

### Field definition details<a name="field-definition-details"></a>

The field definition defines the source, destination \(target\), and type of field\. For example:

```
"Fields": {
        "{fieldName}": {
            "Source": "{source}",
            "Target": "{target}",
            "ContentType": "{contentType}"
        }, ...
    }, ...
```
+ `Source`: This can be a JSON accessor for the field or a Handlebar macro for generating the value of the field\. 

  The source object being parsed is named ` _source` so all fields in the source fields need to be prefaced by this string\. Only the `_source` object is supported\.

  Use the Handlebar macro solution for generating constants and combining multiple source object fields into a single field\. This is useful for indexing\.
+ `Target`: Specifies where in a standard object type the data of this field should be mapped\.

  Populating the standard profile allows you to use data ingested from any data source with applications built on top of Customer Profiles without any specific knowledge of the format of the data being ingested\. 

  This field is optional\. You might want to define fields solely for the purpose of including them in a key\. 

  The format of this field is always a JSON accessor\. The only supported target object is `_profile`\.
+ `ContentType`: The following values are supported STRING, NUMBER, PHONE\_NUMBER, EMAIL\_ADDRESS, NAME\. If no `ContentType` is specified STRING is assumed\. 

  `ContentType` is used to determine how to index the value so agents can search for it\. For example, if `ContentType` is set to PHONE\_NUMBER, a phone number is processed so agents can search for it in any format: the string "\+15551234567" matches "\(555\)\-123\-4567"\.

### Key definition details<a name="key-definition-details"></a>

A key contains one or more fields that together define a key that can be used to search for objects \(or the profiles they belong to\) using the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API\. The key can also be defined to uniquely identify a profile or uniquely identify the object itself\.

```
"Keys": {
        "{keyName}": [{
            "StandardIdentifiers": [...],
            "FieldNames": [ "{fieldname}", ...]
        }], ...
    }, ...
```

Key names are global to a domain\. If you have two keys, with the same name in two different object type mappings:
+ Those keys should occupy the same namespace
+ They can be used to potentially link profiles together between different objects\. If they match between the objects, Customer Profiles places the two objects in the same profile\. 

To phrase this in another way: keys should have the same key name in a domain if, and only if, the same value means that they are related\. For example, a phone number specified in one type of object would be related to the same phone number specified in another type of object\. An internal identifier specified for an imported object from Salesforce might not be related to another object imported from Marketo, even if they have exactly the same value\.

Keys definitions are used in two ways:
+ Inside of Customer Profiles during ingestion, they are used to figure out what profile the object should be assigned to\. 
+ They allow you to use the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to search for the key value and find the profile\. 

### Standard identifiers<a name="standard-identifiers"></a>

Standard identifiers allow you to set attributes on the key\. Decide which identifiers to use based on how you want the data to be ingested in the profiles\. For example, you mark phone number with the identifier PROFILE\. This means phone number is to be treated as unique identifier\. If Customer Profiles gets two contacts with the same phone number, the contacts are going to be merged into a single profile\. 


| Identifier name | Description | 
| --- | --- | 
|  UNIQUE  | This identifier must be specified by exactly one index for each object type\. This key is used to uniquely identify objects of the object type for either fetching them or if needed update a submitted object at a later date\.  All the fields that make up the UNIQUE keys are required to be specified when submitting a new object or it is rejected\.  | 
|  PROFILE  | This identifier means that this key uniquely identifies a profile\. When this identifier is specified, it means that during ingestion Custom Profiles looks for any profile that has this key associated with it\.  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-object-type-mappings.html)  | 
|  LOOKUP\_ONLY  | This identifier indicates the key is not stored after ingesting the object\. The key is only to be used for determining the profile during ingestion\.  The key value is not not associated with the profile during ingestion, which means it can't be used to allow searching for it or matching later ingested objects to the same key\.  | 
|  NEW\_ONLY  | If the profile does not already exist before the object is ingested, the key is associated with the profile\. Otherwise the key is only used for matching objects to profiles\.   | 
|  SECONDARY  | During the matching of an object to a profile, Customer Profiles first looks up all PROFILE keys that do not have the SECONDARY identifier\. These are considered first\. SECONDARY keys are only considered if no matching profile is found using these keys\.  | 

### How profile assignment works using key definitions<a name="how-profile-assignment-works"></a>

When Customer Profiles ingests the custom object mappings, it processes the key definitions\. The following diagram shows how it processes standard identifiers in key definitions to determine which profile to assign the object to\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-template1.png)

### How keys are added to the index for future look ups<a name="how-keys-are-added-index"></a>

The following diagram shows how Customer Profiles processes the standard identifiers to determine whether to persist the key\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-template2.png)

## Additional properties of object types<a name="additional-properties-object-types"></a>

A property type defines which key should be used to encrypt any data of the object type\.

There is an option that defines if new profiles can be created by the ingestion of this object\. Normally when an object is ingested that cannot be matched to an existing profile, a new profile is created as long as this option is true\. If it is not true then the ingested object is created and written to the domain dead\-letter queue\.

It also contains how long data of this object type should be retained in Customer Profiles\. 

**Note**  
Retention on individual objects is set at the time of ingestion of data\. Changing the retention for a specific object type only applies to new data being ingested\. It does not apply to existing data already ingested\.

## Inferred profiles<a name="inferred-profiles"></a>

When a profile is created by the ingestion of an object that has no fields, the standard profile object of this new profile is empty\. This empty standard profile object is an **inferred profile**\. 

When creating an inferred profile, the following two fields are populated in the standard object from the profile object, if available\.
+ If there is any field defined with the content type of `EMAIL_ADDRESS` in the ingested object then this value will be populated into the `EmailAddress` field of the standard profile\.
+ If there is any field with the content type of `PHONE_NUMBER` in the ingested object then this value will be populated into the `PhoneNumber` field of the standard profile\.

These values are populated into the standard profile even if these fields do not have a target defined in the field definition have a target defined or not when the inferred profile is created\.

### Change behavior of inferred profiles to automatically associate the CTR with one profile found<a name="inferred-profiles-change-behavior"></a>

Run the following command on the CLI:

`aws customer-profiles put-profile-object-type --domain-name {domain} --object-type-name CTR --description "No inferred CTR profiles" —template-id CTR-NoInferred`

## Examples of object type mappings<a name="examples-object-type-mappings"></a>

### An object type mapping that generates a profile<a name="profile-generating-example"></a>

The following example shows data that populates the standard profile\.

Following is the incoming object:

```
{
  "account": 1234,
  "email": "john@examplecorp.com",
  "address": {
     "address1": "Street",
     "zip": "Zip",
     "city": "City"
  },
  "firstName": "John",
  "lastName": "Doe"
}
```

The following code shows that incoming object mapping into a standard profile object and indexing `PersonalEmailAddress`, `fullName`, and `accountId`, which is a unique key\.

```
{
    "Fields": {
        "accountId": {
            "Source": "_source.account",
            "Target": "_profile.AccountNumber",
            "ContentType": "NUMBER"
        },
        "shippingAddress.address1": {
            "Source": "_source.address.address1",
            "Target": "_profile.ShippingAddress.Address1"
        },
        "shippingAddress.postalCode": {
            "Source": "_source.address.zip",
            "Target": "_profile.ShippingAddress.PostalCode"
        },
        "shippingAddress.city": {
            "Source": "_source.address.city",
            "Target": "_profile.ShippingAddress.City"
        },
        "personalEmailAddress": {
            "Source": "_source.email",
            "Target": "_profile.PersonalEmailAddress",
            "ContentType": "EMAIL_ADDRESS"
        },
        "fullName": {
            "Source": "{{_source.firstName}} {{_source.lastName}}"
        },
        "firstName": {
            "Source": "_source.firstName",
            "Target": "_profile.FirstName"
        },
        "lastName": {
            "Source": "_source.lastName",
            "Target": "_profile.LastName"
        }
    },
    "Keys": {
        "_email": [
            {
                "FieldNames": ["personalEmailAddress"]
            }
        ],
        "_fullName": [
            {
                "FieldNames": ["fullName"]
            }
        ],
        "_account": [
            {
                "StandardIdentifiers": ["PROFILE","UNIQUE"],
                "FieldNames": ["accountId"]
            }
        ]
    }
}
```

Note that `email` and `fullname` are indexed, but they aren't used to search for the profile\. The account is the unique key\. It is required to specify the object\. Any time an object with the same account ID is ingested it overwrites the previous object with the same account ID\.

Several fields are populated in the standard profile object \(see the fields that have `Target` defined\)\.

### An object type mapping that doesn't populate the standard profile<a name="ticket-issue-example"></a>

This example shows a more complicated use case\. It ingests data related to a profile but it doesn't necessarily populate the standard profile object\.

Following is the incoming object:

```
{
  "email": "john@examplecorp.com",
  "timestamp": "2010-01-01T12:34:56Z",
  "subject": "Whatever this is about",
  "body": "Body of ticket"
}
```

Following is one way of mapping this data:

```
{
    "Fields": {
        "email": {
            "Source": "_source.email",
            "ContentType": "EMAIL_ADDRESS"
        },
        "timestamp": {
            "Source": "_source.timestamp",
            "Target": "_profile.ShippingAddress.Address1"
        }
    },
    "Keys": {
        "_email": [
            {
                "StandardIdentifiers": ["PROFILE","LOOKUP_ONLY"],
                "FieldNames": ["email"]
            }
        ],
        "ticketEmail": [
            {
                "StandardIdentifiers": ["PROFILE","SECONDARY","NEW_ONLY"],
                "FieldNames": ["email"]
            }
        ],
        "uniqueTicket": [
            {
                "StandardIdentifiers": ["UNIQUE"],
                "FieldNames": ["email","timestamp"]
            }
        ]
    }
}
```

This example ingests the data and, at first lookup, it ingests the email address\. 
+ If the email address matches a single profile, it is used to attach the data to that specific profile\. The unique identifier for the ticket is comprised of the email and the timestamp since no other unique identifier exists\.
+ If no profile exists with the specified email, a new profile is created with the single field of `EmailAddress` filled in\. The ingested object is attached to this new **inferred profile**\. The two searchable keys that can find the profile are `_email` and `uniqueTicket`\.
+ If more than one profile exists with the specified email address, a new profile is created with the single field of `EmailAddress` filled in and the object is attached to this new profile\. This profile is created with the `ticketEmail` key defined, in addition to `_email` and `uniqueTicket`\. Any subsequent tickets from that email are assigned to this new **inferred profile**\. The reason for this is that the ` _email` key is referring to three profiles and is thus discarded, however the `ticketEmail` key only refers to a single profile \(the new inferred one\) and is still valid\.
+ In cases where a new **inferred profile** is created, the `EmailAddress` field is populated from the first object that created it\.

## Implicit profile object types<a name="implicit-profile-object-types"></a>

You can use any object type that matches the name of a template ID \(as returned by the [ListProfileObjectTypeTemplates](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjectTypeTemplates.html) API\) without explicitly defining it\. The object type will exactly match the definition of the template definition of this object type\. If an explicit object type is defined, it replaces the implicit one\. 

Implicit object types are included in the [ListProfileObjectTypes](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjectTypes.html) API or returned by [GetProfileObjectType](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetProfileObjectType.html) operations, but they can still be deleted if you want to remove all data ingested from that object type\.