# Standard identifiers<a name="standard-identifiers"></a>

Standard identifiers allow you to set attributes on the key\. Decide which identifiers to use based on how you want the data to be ingested in the profiles\. For example, you mark phone number with the identifier PROFILE\. This means phone number is to be treated as unique identifier\. If Customer Profiles gets two contacts with the same phone number, the contacts are going to be merged into a single profile\. 


| Identifier name | Description | 
| --- | --- | 
|  UNIQUE  | This identifier must be specified by exactly one index for each object type\. This key is used to uniquely identify objects of the object type for either fetching them or if needed update a submitted object at a later date\.  All the fields that make up the UNIQUE keys are required to be specified when submitting a new object or it is rejected\.  | 
|  PROFILE  | This identifier means that this key uniquely identifies a profile\. When this identifier is specified, it means that during ingestion Custom Profiles looks for any profile that has this key associated with it\.  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/standard-identifiers.html)  | 
|  LOOKUP\_ONLY  | This identifier indicates the key is not stored after ingesting the object\. The key is only to be used for determining the profile during ingestion\.  The key value is not not associated with the profile during ingestion, which means it can't be used to allow searching for it or matching later ingested objects to the same key\.  | 
|  NEW\_ONLY  | If the profile does not already exist before the object is ingested, the key is associated with the profile\. Otherwise the key is only used for matching objects to profiles\.   | 
|  SECONDARY  | During the matching of an object to a profile, Customer Profiles first looks up all PROFILE keys that do not have the SECONDARY identifier\. These are considered first\. SECONDARY keys are only considered if no matching profile is found using these keys\.  | 