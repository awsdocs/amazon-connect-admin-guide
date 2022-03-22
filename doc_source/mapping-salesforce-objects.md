# Mapping Salesforce objects to the standard profile<a name="mapping-salesforce-objects"></a>

This topic lists which fields in Salesforce objects map to fields inthe standard profile object in Customer Profiles\.

## Salesforce\-Account object<a name="salesforceaccountobject"></a>

Following is a list of all the fields in a Salesforce\-Account object\. The fields in your Salesforce\-Account object may vary depending on the configuration of your Salesforce instance\.
+ Id
+ IsDeleted
+ MasterRecordId
+ Name
+ Type
+ ParentId
+ BillingStreet
+ BillingCity
+ BillingState
+ BillingPostalCode
+ BillingCountry
+ BillingLatitude
+ BillingLongitude
+ BillingGeocodeAccuracy
+ BillingAddress\.City
+ BillingAddress\.Country
+ BillingAddress\.geocodeAccuracy
+ BillingAddress\.latitude
+ BillingAddress\.longitude
+ BillingAddress\.postalCode
+ BillingAddress\.state
+ BillingAddress\.street
+ ShippingStreet
+ ShippingCity
+ ShippingState
+ ShippingPostalCode
+ ShippingCountry
+ ShippingLatitude
+ ShippingLongitude
+ ShippingGeocodeAccuracy
+ ShippingAddress\.city
+ ShippingAddress\.country
+ ShippingAddress\.latitude
+ ShippingAddress\.longitude
+ ShippingAddress\.postalCode
+ ShippingAddress\.state
+ ShippingAddress\.street
+ Phone
+ Fax
+ AccountNumber
+ Website
+ PhotoUrl
+ Sic
+ Industry
+ AnnualRevenue
+ NumberOfEmployees
+ Ownership
+ TickerSymbol
+ Description
+ Rating
+ Site
+ OwnerId
+ CreatedDate
+ CreatedById
+ LastModifiedDate
+ LastModifiedId
+ SystemModstamp
+ LastActivityDate
+ LastViewedDate
+ LastReferencedDate
+ Jigsaw
+ JigsawCompanyId
+ CleanStatus
+ AccountSource
+ DunsNumber
+ Tradestyle
+ NaicsCode
+ NaicsDesc
+ YearStarted
+ SicDesc
+ DandbCompanyId
+ IsBuyer

## Mapping a Salesforce\-Account object to a standard profile<a name="mapping-salesforceaccountobject"></a>

A subset of the fields in the Salesforce\-Account object map to the standard profile object in Customer Profiles\. 

The following table lists which fields can be mapped from the Salesforce\-Account object to the standard profile\. \(The table includes the mapping for a Salesforce instance that has been configured to include Person fields\.\)


| Salesforce\-Account source field | Standard profile target field | 
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

The Salesforce\-Account customer data from the Salesforce object is associated with an Amazon Connect customer profile using the indexes in the following table\. 


| Standard Index Name | Salesforce\-Account source field | 
| --- | --- | 
|  \_salesforceAccountId  | Id  | 

For example, you can use `_salesforceAccountId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find a profile\. You can find the Salesforce\-Account objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Salesforce-Account`\.

## Salesforce\-Contact object<a name="salesforcecontactobject"></a>

Following is a list of all the fields in a Salesforce\-Contact object\.
+ Id
+ IsDeleted
+ MasterRecordId
+ Accountd
+ LastName
+ FirstName
+ Salutation
+ Name
+ OtherStreet
+ OtherCity
+ OtherState
+ OtherPostalCode
+ OtherCountry
+ OtherLatitude
+ OtherLongitude
+ OtherGeocodeAccuracy
+ OtherAddress\.city
+ OtherAddress\.country
+ OtherAddress\.geocodeAccuracy
+ OtherAddress\.latitude
+ OtherAddress\.postalCode
+ OtherAddress\.state
+ OtherAddress\.street
+ MailingStreet
+ MailingCity
+ MailingState
+ MailingPostalCode
+ MailingCountry
+ MailingLatitude
+ MailingLongitude
+ MailingGeocodeAccuracy
+ MailingAddress\.city
+ MailingAddress\.country
+ MailingAddress\.geocodeAccuracy
+ MailingAddress\.latitude
+ MailingAddress\.longitude
+ MailingAddress\.postalCode
+ MailingAddress\.state
+ MailingAddress\.street
+ Phone
+ Fax
+ MobilePhone
+ HomePhone
+ OtherPhone
+ AssistantPhone
+ ReportsToId
+ Email
+ Title
+ Department
+ AssistantName
+ LeadSource
+ Birthdate
+ Description
+ OwnerId
+ CreatedDate
+ CreatedById
+ LastModifiedDate
+ LastModifiedById
+ SystemModstamp
+ LastActivityDate
+ LastCURequestDate
+ LastCUUpdateDate
+ LastViewedDate
+ LastReferencedDate
+ EmailBouncedReason
+ EmailBouncedDate
+ IsEmailBounced
+ PhotoUrl
+ Jigsaw
+ JigawContactId
+ CleanStatus
+ IndividualId

## Mapping a Salesforce\-Contact object to a standard profile<a name="mapping-salesforcecontactobject"></a>

A subset of the fields in the Salesforce\-Contact object map to the standard profile object in Customer Profiles\. The following table lists which fields can be mapped from the Salesforce\-Contact object to the standard profile object\.


| Salesforce\-Contact source field | Standard profile target field | 
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

The Salesforce\-Contact customer data from a Salesforce object is associated with an Amazon Connect customer profile using the indexes in the following table\. 


| Standard Index Name | Salesforce\-Contact source field | 
| --- | --- | 
|  \_salesforceContactId  | Id  | 
|  \_salesforceAccountId  | AccountId  | 

For example, you can use `_salesforceAccountId` and `_salesforceContactId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find a profile\. You can find the Salesforce\-Contact objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Salesforce-Contact`\.