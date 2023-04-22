# Flow block: Customer profiles<a name="customer-profiles-block"></a>

## Description<a name="customer-profiles-block-description"></a>
+ Enables you to retrieve, create, and update a customer profile\.
+ You can configure the block to retrieve profiles by phone number or email\.
+ When a customer profile is retrieved, the **Response fields** are stored in the contact attributes for that customer\.
+ You can also reference the **Response fields** by using the following JSONPath: `$.Customer.` For example, `$.Customer.City`\.
+ The following examples show how you might use this block:
  + Use a [Play prompt](play.md) block after retrieving a profile to provide a personalized call or chat experience by referencing the supported profile fields\.
  + Use a [Check contact attributes](check-contact-attributes.md) block after retrieving a profile to route a contact based on the value of the profile field\.

## Supported channels<a name="customer-profiles-block-channels"></a>

The following table lists how this block routes a contact that is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="customer-profiles-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flow types

## Properties<a name="customer-profiles-block-properties"></a>

The following image shows the **Properties** page of the **Customer profiles** block\. It is configured to return a customer profile, using the customer phone number to find it\.

![\[The properties page of the Customer profiles block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-block-properties.png)

Under **Action**, choose from the following options: 
+ **Get profile**
+ **Create a profile**
+ **Update a profile**

Use the options under **Response fields** to identify objects that agents can search on when they use the agent application\. 

The **Action** and **Response fields** correspond to the request and response fields of the [Profile](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_Profile.html) API\. 

## Configuration tips<a name="customer-profiles-block-tips"></a>
+ Before using this block, make sure Customer Profiles is enabled for your Amazon Connect instance\. For instructions, see [Use Customer Profiles](customer-profiles.md)\.
+ A contact is routed down the **Error** branch in the following situations:
  + Customer Profiles is not enabled for your Amazon Connect instance\.
  + Request data values are not valid\. The request values cannot be over 255 characters\.
  + The Customer Profiles API request has been throttled\.
  + Customer Profiles is having availability issues\.

## Configured block<a name="customer-profiles-block-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It shows four branches: **Success**, **Error**, **Multiple found**, and **None found**\. 

![\[A configured Customer profiles block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-block-configured.png)