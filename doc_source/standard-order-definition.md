# Standard order definition<a name="standard-order-definition"></a>

The following table lists all the fields in the Customer Profiles standard order object\.


|  |  |  | 
| --- |--- |--- |
| Standard order field | Data type | Description | 
| OrderId | String | The unique identifier of a standard order\. | 
| CustomerEmail | String | The customer's email address\. | 
| CustomerPhone | String | The customer's phone number\. | 
| CreatedDate | String | The order's date created\. | 
| UpdatedDate | String | The order's date updated\. | 
| ProcessedDate | String | The order's date processed\. | 
| ClosedDate | String | The order's date closed\. | 
| CancelledDate | String | The order's date cancelled\. | 
| CancelReason | String | The order's cancel reason\. | 
| Name | String | The order's name\. | 
| AdditionalInformation | String | Any additional information relevant to the order\. | 
| Gateway | String | The order's payment gateway\. | 
| Status | String | The order's status\. | 
| StatusCode | String | The order's status code\. Valid values: DRAFT \| ACTIVATED | 
| StatusUrl | String | The order's status URL\. | 
| CreditCardNumber | String | The customer's credit card last four digits\. | 
| CreditCardCompany | String | The customer's credit card company\. | 
| FulfillmentStatus | String | The order's fulfillment status\. | 
| TotalPrice | String | The order's total price\. | 
| TotalTax | String | The order's total tax\. | 
| TotalDiscounts | String | The order's total discounts\. | 
| TotalItemsPrice | String | The order's total items price\. | 
| TotalShippingPrice | String | The order's total shipping price\. | 
| TotalTipReceived | String | The order's total tip received\. | 
| Currency | String | The order's currency\. | 
| TotalWeight | String | The order's total weight\. | 
| BillingAddress | OrderAddress | The customer's billing address\. | 
| ShippingAddress | OrderAddress | The customer's shipping address\. | 
| OrderItems | OrderItem list | The order's items\. | 
| Attributes | String\-to\-string map | Key\-value pair of attributes of a standard order\. | 

## OrderAddress data type<a name="orderaddress-data-type"></a>


|  |  |  | 
| --- |--- |--- |
| Standard order field | Data type | Description | 
| Name | String | The name associated with an order address\. | 
| Address1 | String | The first line of an order address\. | 
| Address2 | String | The second line of an order address\. | 
| Address3 | String | The third line of an order address\. | 
| Address4 | String | The fourth line of an order address\. | 
| City | String | The city of an order address\. | 
| County | String | The county of an order address\. | 
| State | String | The state of an order address\. | 
| Province | String | The province of an order address\. | 
| Country | String | The country of an order address\. | 
| PostalCode | String | The postal code of an order address\. | 

## OrderItem data type<a name="orderitem-data-type"></a>


|  |  |  | 
| --- |--- |--- |
| Standard order field | Data type | Description | 
| Title | String | The title of an order item\. | 
| Price | String | The price of an order item\. | 
| Quantity | String | The quantity of an order item\. | 