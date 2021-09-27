# Standard profile definition<a name="standard-profile-definition"></a>

The following table lists all the fields in the Customer Profiles standard profile\. object\.


| Standard profile field | Data type | Description | 
| --- | --- | --- | 
|  ProfileId  | String  | The unique identifier of a customer profile\.  | 
|  AccountNumber  | String  | A unique account number that you have given to the customer\. | 
|  AdditionalInformation  | String  | Any additional information relevant to the customer's profile\. | 
|  PartyType  | String  | The type of profile used to describe the customer\. Valid values: INDIVIDUAL \| BUSINESS \| OTHER | 
|  BusinessName  | String  | The name of the customer's business\. | 
|  FirstName  | String  | The customer's first name\. | 
|  MiddleName  | String  | The customer's middle name\. | 
|  LastName  | String  | The customer's last name\. | 
|  BirthDate  | String  | The customer's birth date\. | 
|  Gender  | String  | The gender with which the customer identifies\. | 
|  PhoneNumber  | String  | The customer's phone number, which has not been specified as a mobile, home, or business number\. | 
|  MobilePhoneNumber  | String  | The customer's mobile phone number\. | 
|  HomePhoneNumber  | String  | The customer's home phone number\. | 
|  BusinessPhoneNumber  | String  | The customer's business phone number\. | 
|  EmailAddress  | String  | The customer’s email address, which has not been specified as a personal or business address\. | 
|  BusinessEmailAddress  | String  | The customer’s business email address\. | 
|  Address  | Address  | A generic address associated with the customer that is not mailing, shipping, or billing\. | 
|  ShippingAddress  | Address  | The customer's shipping address\. | 
|  MailingAddress  | Address  | The customer's mailing address\. | 
|  BillingAddress  | Address  | The customer's billing address\. | 
|  Attributes  | String\-to\-string map  | Key\-value pair of attributes of a customer profile\. | 

## Address data type<a name="address-data-type"></a>


| Standard profile field | Data type | Description | 
| --- | --- | --- | 
|  Address1  | String  | The first line of a customer address\.  | 
|  Address2  | String  | The second line of a customer address\.  | 
|  Address3  | String  | The third line of a customer address\.  | 
|  Address4  | String  | The fourth line of a customer address\.  | 
|  City  | String  | The city in which the customer lives\.  | 
|  Country  | String  | The country in which the customer lives\.  | 
|  County  | String  | The county in which the customer lives\.  | 
|  PostalCode  | String  | The postal code of the customer address\.  | 
|  Province  | String  | The province in which the customer lives\.  | 
|  State  | String  | The state in which the customer lives\.  | 