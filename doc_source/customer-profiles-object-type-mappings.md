# Create and ingest customer data into Customer Profiles by using Amazon S3<a name="customer-profiles-object-type-mappings"></a>

You can define data from any source using Amazon S3 and seamlessly enrich a customer profile without the need for custom or pre\-built integrations\. For example, say you want to provide agents with relevant purchase history information\. You can import purchase transaction data from an internal application into a spreadsheet file on S3 and then link it to a customer profile\.

To set this up, you need to define an [object type mapping](customer-profiles-object-type-mapping.md) that describes what the custom profile object looks like\. This mapping defines how fields from your data can be used to either populate fields in the standard profile or how it can be used to assign the data to a specific profile\. 

After you create the object type mapping, you can use the [PutProfileObject](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutProfileObject.html) API to upload the custom profile data from your CRM into the custom profile object\. 