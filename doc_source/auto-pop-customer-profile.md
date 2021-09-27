# Use contact attributes to autopopulate customer profiles<a name="auto-pop-customer-profile"></a>

By default, Amazon Connect Customer Profiles uses the following values to search for and autopopulate a customer profile in its user interface: 
+ For voice contacts: Phone number
+ For chat contacts: Customer name

To customize this behavior, use the following contact attributes:


| Attribute | Description | Type | JSONPath Reference | 
| --- | --- | --- | --- | 
| profileSearchKey | The name of the attribute you want to use to search for a profile\.  | User\-defined | Not applicable | 
| profileSearchValue | The value of the key you want to search for, such as customer name or account number\.  | User\-defined | Not applicable | 

For example, to search by email for chat contacts, you can set the `profileSearchKey` attribute to the `_email` search key, and provide the email value as the `profileSearchValue`\. 

If you have defined custom keys in your profile objects, you can search by those search keys as well\. To make sure your custom keys are searchable, see [Key definition details](object-type-mapping-definition-details.md#key-definition-details)\.

The following image shows how you might use these attributes in the [Set contact attributes](set-contact-attributes.md) block\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-attributes1.png)