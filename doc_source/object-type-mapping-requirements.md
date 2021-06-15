# Object type mapping requirements<a name="object-type-mapping-requirements"></a>

The following information needs to be in your object type mapping so Customer Profiles can process the incoming data: 
+ A definition of all the fields in the ingested object that should be mapped to the standard profile, or used for assigning the data to a profile\. This tells Customer Profiles which fields in the ingested **source** object should be mapped to given fields in the standard profile object\.
+ Which fields in the source object from your custom data should be indexed and how\. 

  When the source data is ingested by Customer Profiles, the indexed fields determine:
  + Which profile a specific object belongs to\.
  + Which objects are related to each other and should be placed in the same profile\. For example, an account number or a CTR contact ID\. 
  + What values can be used to find a profile\. For example, the contact's name can be indexed\. This would allow agents to find all profiles that belong to customers with a specific name\. 

## Key requirements<a name="key-requirements"></a>

You must define at least one key\. Customer Profiles uses this key to map your custom profile object to a profile\.

The custom profile object mapping also needs at least one key that uniquely identifies the object so that it can be updated by specifying the same value of this field \(these requirements can be satisfied with a single key\)\.

Each key can be made up of one or more fields\. 

## Field requirements<a name="field-requirements"></a>

A field definition specifies how to read a value for that field name from a source object\. The field definition also specifies what kind of data is stored in the field\.

Object type names can be any alpha numerical string or the '\-' and '\_' character, they also cannot start with a '\_' character, which is used for reserved standard object types\.