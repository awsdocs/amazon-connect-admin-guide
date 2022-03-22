# Mapping ServiceNow objects to the standard profile object<a name="mapping-servicenow-objects"></a>

This topic lists which fields in ServiceNow objects map to fields in the standard profile object in Amazon Connect Customer Profiles\.

## Servicenow\-sys\_user object<a name="servicenow-sys-user-object"></a>

Following is a list of all the fields in a Servicenow\-sys\_user object
+ sys\_id
+ active
+ building
+ calendar\_integration
+ city
+ company
+ cost\_center
+ country
+ date\_format
+ default\_perspective
+ department
+ edu\_status
+ email
+ employee\_number
+ enable\_multifactor\_authn
+ failed\_attempts
+ first\_name
+ gender
+ home\_phone
+ internal\_integration\_user
+ introduction
+ last\_login
+ last\_login\_device
+ last\_login\_time
+ last\_name
+ last\_password
+ ldap\_server
+ location
+ locked\_out
+ manager
+ middle\_name
+ mobile\_phone
+ name
+ notification
+ password\_needs\_reset
+ phone
+ photo
+ preferred\_language
+ roles
+ schedule
+ source
+ state
+ street
+ sys\_class\_name
+ sys\_created\_by
+ sys\_created\_on
+ sys\_domain\.link
+ sys\_domain\.value
+ sys\_domain\_path
+ sys\_id
+ sys\_mod\_count
+ sys\_updated\_by
+ sys\_udpated\_on
+ time\_format
+ time\_zone
+ title
+ user\_name
+ user\_password
+ web\_service\_access\_only
+ zip

## Mapping Servicenow\-sys\_users to a standard profile object<a name="mapping-servicenow-sys-user-object"></a>

A subset of the fields in the Servicenow\-sys\_users object map to the standard profile object in Customer Profiles\. 

The following table lists which fields can be mapped from the Servicenow\-sys\_users object to the standard profile\.


| Servicenow\-sys\_users source field | Customer profiles target field | 
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

The Servicenow\-sys\_user customer data from Servicenow object is associated with an Amazon Connect customer profile using the indexes in the following table\. 


| Standard Index Name | Servicenow\-sys\_user source field | 
| --- | --- | 
|  \_serviceNowSystemId  | sys\_id  | 

For example, you can use `_serviceNowSystemId` and `_serviceNowIncidentId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find an Amazon Connect customer profile\. You can find the Servicenow\-sys\_user objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Servicenow-sys_user`\.