# Mapping Marketo objects to the standard profile<a name="mapping-marketo-objects"></a>

This topic lists which fields in Marketo objects map to fields in the standard profile object in Customer Profiles\.

## Marketo\-leads object<a name="marketo-objects"></a>

Following is a list of all the fields in a Marketo\-leads object
+ id
+ firstName
+ lastName
+ middleName
+ email
+ phone
+ mobilePhone
+ billingStreet
+ billingCity
+ billingState
+ billingCountry
+ billingPostalCode
+ address
+ city
+ state
+ country
+ postalcode
+ gender
+ dateOfBirth

## Mapping Marketo\-leads to a standard profile<a name="mapping-marketo-leads-object"></a>

A subset of fields in the Marketo\-leads object map to the standard profile\.


| Marketo\-leads source field | Standard profile target field | 
| --- | --- | 
|  id  | Attributes\.MarketoLeadId  | 
|  sfdcAccountId  | Attributes\.sfdcAccountId  | 
|  sfdcContactId  | Attributes\.sfdcContactId  | 
|  firstName  | FirstName  | 
|  lastName  | LastName  | 
|  middleName  | MiddleName  | 
|  email  | EmailAddress  | 
|  phone  | PhoneNumber  | 
|  mobilePhone  | MobilePhoneNumber  | 
|  mobilePhone  | MobilePhoneNumber  | 
|  billingStreet  | BillingAddress\.Address1  | 
|  billingCity  | BillingAddress\.City  | 
|  billingState  | BillingAddress\.State  | 
|  billingCountry  | BillingAddress\.Country  | 
|  billingPostalCode  | BillingAddress\.PostalCode  | 
|  address  | Address\.Address1  | 
|  city  | Address\.City  | 
|  state  | Address\.State  | 
|  country  | Address\.Country  | 
|  postalcode  | Address\.PostalCode  | 
|  gender  | Gender  | 
|  dataOfBirth  | BirthDate  | 

The Marketo\-leads customer data from Marketo is associated with an Amazon Connect customer profile using the indexes in the following table\. 


| Standard Index Name | Marketo\-leads source field | 
| --- | --- | 
|  \_marketoLeadId  | id  | 
|  \_salesforceAccountId  | sfdcAccountId  | 
|  \_salesforceContactId  | sfdcContactId  | 

For example, you can use `_marketoLeadId`, `_salesforceAccountId`, and `_salesforceContactId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find an Amazon Connect customer profile\. You can find the Marketo\-leads objects associated with a specific customer profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Marketo-leads`\.