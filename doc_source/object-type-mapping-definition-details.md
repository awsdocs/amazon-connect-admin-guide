# Object type mapping definition details<a name="object-type-mapping-definition-details"></a>

The object type mapping definition has two parts: the field definition and the key definition\. 

## Field definition details<a name="field-definition-details"></a>

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

## Key definition details<a name="key-definition-details"></a>

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