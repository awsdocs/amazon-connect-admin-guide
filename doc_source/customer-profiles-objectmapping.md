# Object mapping for Customer Profiles<a name="customer-profiles-objectmapping"></a>

Following is the object mapping from the external applications to the standard profile attributes in Amazon Connect Customer Profiles\. 

## Salesforce objects<a name="cp-objectmapping-salesforce"></a>

**Object: Account**


| Saleforce source field | Customer profiles target field | 
| --- | --- | 
|  Id  | Attributes\.sfdcAccountId  | 
|  Name  | BusinessName  | 
|  Phone  | PhoneNumber  | 
|  BillingStreet  | BillingAddress\.Address1  | 
|  BillingCity  | BillingAddress\.City  | 
|  BillingState  | BillingAddress\.State  | 
|  BillingCountry  | BillingAddress\.Country  | 
|  BillingPostalCode  | BillingAddress\.PostalCode  | 
|  ShippingStreet  | ShippingAddress\.Address1  | 
|  ShippingCity  | ShippingAddress\.City  | 
|  ShippingState  | ShippingAddress\.State  | 
|  ShippingCountry  | ShippingAddress\.Country  | 
|  ShippingPostalCode  | ShippingAddress\.PostalCode  | 
|  IsPersonAccount  | PartyType  | 
|  PersonMobilePhone  | MobilePhoneNumber  | 
|  PersonHomePhone  | HomePhoneNumber  | 
|  PersonEmail  | PersonalEmailAddress  | 
|  PersonMailingAddress\.Street  | MailingAddress\.Address1  | 
|  PersonMailingAddress\.City  | MailingAddress\.City  | 
|  PersonMailingAddress\.State  | MailingAddress\.State  | 
|  PersonMailingAddress\.Country  | MailingAddress\.Country  | 
|  PersonMailingAddress\.PostalCode  | MailingAddress\.PostalCode  | 
|  PersonBirthDate  | BirthDate  | 
|  PersonOtherStreet  | Address\.Address1  | 
|  PersonOtherCity  | Address\.City  | 
|  PersonOtherState  | Address\.State  | 
|  PersonOtherCountry  | Address\.Country  | 
|  PersonOtherPostalCode  | Address\.PostalCode  | 
|  FirstName  | FirstName  | 
|  LastName  | LastName  | 
|  MiddleName  | MiddleName  | 
|  AccountNumber  | AccountNumber  | 

**Object: Contact**


| Saleforce source field | Customer profiles target field | 
| --- | --- | 
|  Id  | Attributes\.sfdcContactId  | 
|  AccountId  | Attributes\.sfdcAccountId  | 
|  LastName  | LastName  | 
|  FirstName  | FirstName  | 
|  MiddleName  | MiddleName  | 
|  OtherStreet  | Address\.Address1  | 
|  OtherCity  | Address\.City  | 
|  OtherState  | Address\.State  | 
|  OtherCountry  | Address\.Country  | 
|  OtherPostalCode  | Address\.PostalCode  | 
|  MailingStreet  | MailingAddress\.Address1  | 
|  MailingCity  | MailingAddress\.City  | 
|  MailingState  | MailingAddress\.State  | 
|  MailingCountry  | MailingAddress\.Country  | 
|  MailingPostalCode  | MailingAddress\.PostalCode  | 
|  Phone  | PhoneNumber  | 
|  HomePhone  | HomePhoneNumber  | 
|  MobilePhone  | MobilePhoneNumber  | 
|  Email  | EmailAddress  | 
|  Birthdate  | BirthDate  | 

## Zendesk objects<a name="cp-objectmapping-zendesk"></a>

**Object: users**


| Zendesk source field | Customer profiles target field | 
| --- | --- | 
|  id  | Attributes\.ZendeskUserId  | 
|  external\_id  | Attributes\.ZendeskExternalId  | 
|  email  | EmailAddress  | 
|  phone  | PhoneNumber  | 

## Marketo objects<a name="cp-objectmapping-marketo"></a>

**Object: leads**


| Marketo source field | Customer profiles target field | 
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

## ServiceNow objects<a name="cp-objectmapping-servicenow"></a>

**Object: sys\_user**


| ServiceNow source field | Customer profiles target field | 
| --- | --- | 
|  sys\_id  | Attributes\.ServiceNowSystemId  | 
|  first\_name  | FirstName  | 
|  last\_name  | LastName  | 
|  middle\_name  | MiddleName  | 
|  gender  | Gender  | 
|  email  | EmailAddress  | 
|  phone  | PhoneNumber  | 
|  home\_phone  | HomePhoneNumber  | 
|  mobile\_phone  | MobilePhoneNumber  | 
|  street  | Address\.Address1  | 
|  city  | Address\.City  | 
|  state  | Address\.State  | 
|  country  | Address\.Country  | 
|  zip  | Address\.PostalCode  | 