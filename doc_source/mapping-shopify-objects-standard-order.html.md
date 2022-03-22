# Mapping Shopify objects to the standard order<a name="mapping-shopify-objects-standard-order.html"></a>

This topic lists which fields in Shopify objects map to fields in the standard order object in Customer Profiles\.

## Shopify\-DraftOrder object<a name="shopify-draftorder-object.html"></a>

For a list of all the fields in a Shopify\-DraftOrder object see [The DraftOrder object](https://shopify.dev/api/admin-rest/2021-10/resources/draftorder#resource_object) in the Shopify documentation\.

## Mapping a Shopify\-DraftOrder object to a standard order<a name="shopify-draftorder-object-standardorder.html"></a>

A subset of the fields in the Shopify\-DraftOrder object map to the standard order object in Customer Profiles\.

The following table lists which fields can be mapped from the Shopify\-DraftOrder object to the standard order\.

 The `StatusCode` is `ACTIVATED` if `order_status_url` exists in the source\. Otherwise, the `StatusCode` is `DRAFT`\.


|  |  | 
| --- |--- |
| Shopify\-DraftOrder source field | Standard order target field | 
| id | Attributes\.ShopifyOrderId | 
| customer\.id | Attributes\.ShopifyCustomerId | 
| note | AdditionalInformation | 
| email | CustomerEmail | 
| currency | Currency | 
| created\_at | CreatedDate | 
| updated\_at | UpdatedDate | 
| name | Name | 
| status | Status | 
| order\_status\_url | StatusCode | 
| billing\_address\.address1 | BillingAddress\.Address1 | 
| billing\_address\.address2 | BillingAddress\.Address2 | 
| billing\_address\.city | BillingAddress\.City | 
| billing\_address\.zip | BillingAddress\.PostalCode | 
| billing\_address\.province | BillingAddress\.Province | 
| billing\_address\.country | BillingAddress\.Country | 
| billing\_address\.name | BillingAddress\.Name | 
| shipping\_address\.address1 | ShippingAddress\.Address1 | 
| shipping\_address\.address2 | ShippingAddress\.Address2 | 
| shipping\_address\.city | ShippingAddress\.City | 
| shipping\_address\.zip | ShippingAddress\.PostalCode | 
| shipping\_address\.province | ShippingAddress\.Province | 
| shipping\_address\.country | ShippingAddress\.Country | 
| shipping\_address\.name | ShippingAddress\.Name | 
| invoice\_url | StatusUrl | 
| total\_price | TotalPrice | 
| total\_tax | TotalTax | 
| line\_items\[\]\.title | OrderItems\[\]\.Title | 
| line\_items\[\]\.price | OrderItems\[\]\.Price | 
| line\_items\[\]\.quantity | OrderItems\[\]\.Quantity | 

### Example<a name="example-shopify-draftorder-object-standardorder.html"></a>

The following example shows how to map a source field to a target field\.

```
"shopifyOrderId": {
    "Source": "_source.detail.event.detail.payload.id",
    "Target": "_order.Attributes.ShopifyOrderId"
}
```

The Shopify\-DraftOrder customer data from the Shopify object is associated with an Amazon Connect standard order using the following index\.


|  |  | 
| --- |--- |
| Standard Index Name | Shopify\-DraftOrder source field | 
| \_shopifyOrderId | id | 

For example, you can use `_shopifyOrderId` as an `ObjectFilter.KeyName` with the the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API to find a standard order\. You can find the Shopify\-DraftOrder objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Shopify-DraftOrder`\.

## Shopify\-Order object<a name="shopify-order-object.html"></a>

For a list of all the fields in a Shopify\-Order object see [The Order object](https://shopify.dev/api/admin-rest/2021-10/resources/order#resource_object) in the Shopify documentation\.

## Mapping a Shopify\-Order object to a standard order<a name="mapping-shopify-order-object-standarorder.html"></a>

A subset of the fields in the Shopify\-Order object map to the standard order object in Customer Profiles\.

The following table lists which fields can be mapped from the Shopify\-Order object to the standard order\.

The `StatusCode` is `ACTIVATED` if `order_status_url` exists in the source\. Otherwise, the `StatusCode` is `DRAFT`\.


|  |  | 
| --- |--- |
| Shopify\-Order source field | Standard order target field | 
| id | Attributes\.ShopifyOrderId | 
| customer\.id | Attributes\.ShopifyCustomerId | 
| cancelled\_at | CancelledDate | 
| cancel\_reason | CancelReason | 
| closed\_at | ClosedDate | 
| created\_at | CreatedDate | 
| currency | Currency | 
| email | CustomerEmail | 
| financial\_status | Status | 
| order\_status\_url | StatusCode | 
| fulfillment\_status | FulfillmentStatus | 
| gateway | Gateway | 
| name | Name | 
| note | AdditionalInformation | 
| order\_status\_url | StatusUrl | 
| phone | CustomerPhone | 
| processed\_at | ProcessedDate | 
| total\_discounts | TotalDiscounts | 
| total\_line\_items\_price | TotalItemsPrice | 
| total\_price | TotalPrice | 
| total\_shipping\_price\_set\.shop\_money\.amount | TotalShippingPrice | 
| total\_tax | TotalTax | 
| total\_tip\_received | TotalTipReceived | 
| total\_weight | TotalWeight | 
| updated\_at | UpdatedDate | 
| billing\_address\.address1 | BillingAddress\.Address1 | 
| billing\_address\.address2 | BillingAddress\.Address2 | 
| billing\_address\.city | BillingAddress\.City | 
| billing\_address\.zip | BillingAddress\.PostalCode | 
| billing\_address\.province | BillingAddress\.Province | 
| billing\_address\.country | BillingAddress\.Country | 
| billing\_address\.name | BillingAddress\.Name | 
| payment\_details\.credit\_card\_number | CreditCardNumber | 
| payment\_details\.credit\_card\_company | CreditCardCompany | 
| shipping\_address\.address1 | ShippingAddress\.Address1 | 
| shipping\_address\.address2 | ShippingAddress\.Address2 | 
| shipping\_address\.city | ShippingAddress\.City | 
| shipping\_address\.zip | ShippingAddress\.PostalCode | 
| shipping\_address\.province | ShippingAddress\.Province | 
| shipping\_address\.country | ShippingAddress\.Country | 
| shipping\_address\.name | ShippingAddress\.Name | 
| line\_items\[\]\.title | OrderItems\[\]\.Title | 
| line\_items\[\]\.price | OrderItems\[\]\.Price | 
| line\_items\[\]\.quantity | OrderItems\[\]\.Quantity | 

### Example<a name="example-shopify-draftorder-object-standardorder.html"></a>

The following example shows how to map a source field to a target field\.

```
"shopifyOrderId": {
    "Source": "_source.detail.event.detail.payload.id",
    "Target": "_order.Attributes.ShopifyOrderId"
}
```

The Shopify\-Order customer data from the Shopify object is associated with an Amazon Connect standard order using the following index\.


|  |  | 
| --- |--- |
| Standard Index Name | Shopify\-Order source field | 
| \_shopifyOrderId | id | 

For example, you can use `_shopifyOrderId` as an `ObjectFilter.KeyName` with the the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API to find a standard order\. You can find the Shopify\-Order objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Shopify-Order`\.