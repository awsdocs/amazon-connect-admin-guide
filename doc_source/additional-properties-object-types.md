# Additional properties of object types<a name="additional-properties-object-types"></a>

A property type defines which key should be used to encrypt any data of the object type\.

There is an option that defines if new profiles can be created by the ingestion of this object\. Normally when an object is ingested that cannot be matched to an existing profile, a new profile is created as long as this option is true\. If it is not true then the ingested object is created and written to the domain dead\-letter queue\.

It also contains how long data of this object type should be retained in Customer Profiles\. 

**Note**  
Retention on individual objects is set at the time of ingestion of data\. Changing the retention for a specific object type only applies to new data being ingested\. It does not apply to existing data already ingested\.