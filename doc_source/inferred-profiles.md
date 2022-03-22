# Inferred profiles<a name="inferred-profiles"></a>

When a profile is created by the ingestion of an object that has no fields, the standard profile object of this new profile is empty\. This empty standard profile object is an **inferred profile**\. 

When creating an inferred profile, the following two fields are populated in the standard object from the profile object, if available\.
+ If there is any field defined with the content type of `EMAIL_ADDRESS` in the ingested object then this value will be populated into the `EmailAddress` field of the standard profile\.
+ If there is any field with the content type of `PHONE_NUMBER` in the ingested object then this value will be populated into the `PhoneNumber` field of the standard profile\.

Values for these fields are populated into the standard profile even if the fields do not have a target defined in the field definition\.