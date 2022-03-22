# Mapping Shopify objects to the standard profile object<a name="mapping-shopify-objects"></a>

This topic lists which fields in Shopify objects map to fields in the standard profile object in Amazon Connect Customer Profiles\.

## Shopify\-Customer object<a name="shopify-identify-object"></a>

Following is a list of all the fields in a Shopify\-Customer object\.


+ accepts\_marketing
+ accepts\_marketing\_updated\_at
+ addresses
+ currency
+ created\_at
+ default\_address\.address1
+ default\_address\.address2
+ default\_address\.city
+ default\_address\.company
+ default\_address\.country
+ default\_address\.country\_code
+ default\_address\.country\_name
+ default\_address\.customer\_id
+ default\_address\.default
+ default\_address\.first\_name
+ default\_address\.id
+ default\_address\.last\_name
+ default\_address\.name
+ default\_address\.phone
+ default\_address\.province
+ default\_address\.province\_code
+ default\_address\.zip
+ email
+ first\_name
+ id
+ last\_name
+ last\_order\_id
+ last\_order\_name
+ metafield\.key
+ metafield\.value
+ metafield\.namespace
+ metafield\.value\_type
+ marketing\_opt\_in\_level
+ multipass\_identifier
+ note
+ orders\_count
+ phone
+ sms\_marketing\_consent\.state
+ sms\_marketing\_consent\.opt\_in\_level
+ sms\_marketing\_consent\.consent\_updated\_at
+ sms\_marketing\_consent\.consent\_collected\_from
+ state
+ tags
+ tax\_exempt
+ tax\_exemptions
+ total\_spent
+ updated\_at
+ verified\_email

## Mapping a Shopify\-Customer object to a standard profile<a name="mapping-shopify-customer-object"></a>

A subset of the fields in the Shopify\-Customer object map to the standard profile object in Customer Profiles\. 

The following table lists which fields can be mapped from the Shopify\-Customer object to the standard profile\.


|  |  | 
| --- |--- |
| Shopify\-Customer source field | Standard profile target field | 
| id | Attributes\.ShopifyCustomerId | 
| email | EmailAddress | 
| first\_name | FirstName | 
| last\_name | LastName | 
| note | AdditionalInformation | 
| phone | PhoneNumber | 
| default\_address\.address1 | Address\.Address1 | 
| default\_address\.address2 | Address\.Address2 | 
| default\_address\.city | Address\.City | 
| default\_address\.province | Address\.Province | 
| default\_address\.country | Address\.Country | 
| default\_address\.zip | Address\.PostalCode | 

### Example<a name="example-mapping-shopify-customer-object"></a>

The following example shows how to map a source field to a target field\.

```
"shopifyCustomerId": {
    "Source": "_source.detail.event.detail.payload.id",
    "Target": "_profile.Attributes.ShopifyCustomerId"
}
```

The Shopify\-Customer customer data from the Shopify object is associated with an Amazon Connect customer profile using the following index\.


|  |  | 
| --- |--- |
| Standard Index Name | Shopify\-Customer source field | 
| \_shopifyCustomerId | id | 

For example, you can use `_shopifyCustomerId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find an Amazon Connect customer profile\. You can find the Shopify\-Customer objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Shopify-Customer`\.