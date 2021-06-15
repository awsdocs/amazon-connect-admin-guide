# Mapping Zendesk objects to the standard profile<a name="mapping-zendesk-objects"></a>

This topic lists which fields in Zendesk objects map to fields in the standard profile in Customer Profiles\.

## Zendesk\-users object<a name="zendeskusersobject"></a>

Following is a list of all the fields in a Zendesk\-users object\.
+ id
+ url
+ external\_id
+ email
+ active
+ chat\_only
+ customer\_role\_id
+ role\_type
+ details
+ last\_login\_at
+ locale
+ locale\_id
+ moderator
+ notes
+ only\_private\_comments
+ default\_group\_id
+ phone
+ shared\_phone\_number
+ photo
+ restricted\_agent
+ role
+ shared
+ tags
+ signature
+ suspended
+ ticket\_restriction
+ time\_zone
+ two\_factor\_auth\_enabled
+ user\_fields
+ verified
+ report\_csv
+ created\_at
+ updated\_at

## Mapping Zendesk users to a standard profile<a name="mapping-zendeskusersobject"></a>

A subset of the fields in the Zendesk\-users object map to the standard profile in Customer Profiles\. The following table lists which fields can be mapped from the Zendesk\-users object to the standard profile\.


| Zendesk\-users source field | Standard profile target field | 
| --- | --- | 
|  id  | Attributes\.ZendeskUserId  | 
|  external\_id  | Attributes\.ZendeskExternalId  | 
|  email  | EmailAddress  | 
|  phone  | PhoneNumber  | 

The Zendesk\-users customer data from the Zendesk object is associated with a Amazon Connect customer profile using the following indexes\. 


| Standard Index Name | Zendesk\-user source field | 
| --- | --- | 
|  \_zendeskUserId  | Id  | 
|  \_zendeskExternalId  | external\_id  | 

For example, you can use `_zendeskUserId` and `_zendeskExternalId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find an Amazon Connect customer profile\. You can find the Zendesk\-users objects associated with a specific customer profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Zendesk-users`\.

## Zendesk\-tickets object<a name="cp-standardprofileobject-object-zendesktickets"></a>

No mapping currently exists for the Zendesk\-tickets object into the standard profile, but you can still ingest it\. The data is ingest as is\. Following is an example of the data in the Zendesk\-tickets object\. 
+ id
+ url
+ type
+ subject
+ raw\_subject
+ description
+ priority
+ status
+ recipient
+ requester\_id
+ submitter\_id
+ assignee\_id
+ organization\_id
+ group\_id
+ collaborator\_ids
+ email\_cc\_ids
+ follower\_ids
+ forum\_topic\_id
+ problem\_id
+ has\_incidents
+ due\_at
+ tags
+ via\.channel
+ custom\_fields
+ satisfaction\_rating
+ sharing\_agreement\_ids
+ followup\_ids
+ ticket\_form\_id
+ brand\_id
+ allow\_channelback
+ allow\_attachments
+ is\_public
+ created\_at
+ updated\_at

The Zendesk\-tickets customer data from a Zendesk object is associated with a standard profile using the indexes in the following table\. 


| Standard Index Name | Zendesk\-tickets source field | 
| --- | --- | 
|  \_zendeskTicketId  | Id  | 
|  \_zendeskUserId  | requester\_id  | 

For example, you can use `_zendeskUserId` and `_zendeskExternalId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find an Amazon Connect customer profile\. You can find the Zendesk\-tickets objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Zendesk-tickets`\.