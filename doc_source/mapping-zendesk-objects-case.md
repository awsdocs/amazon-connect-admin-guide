# Mapping Zendesk objects to the standard case<a name="mapping-zendesk-objects-case"></a>

This topic lists which fields in Zendesk objects map to fields in the standard case in Customer Profiles\.

## Zendesk\-tickets object<a name="zendeskticketsobject"></a>

Following is a list of all the fields in a Zendesk\-tickets object\.
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

## Mapping Zendesk\-tickets object to a standard case<a name="mapping-zendeskticketsobject-case"></a>

A subset of the fields in the Zendesk\-tickets object map to the standard case in Customer Profiles\. The following table lists which fields can be mapped from the Zendesk\-tickets object to the standard case\.


| Zendesk\-tickets source field | Standard case target field | 
| --- | --- | 
|  requester\_id  | Attributes\.ZendeskUserId  | 
|  id  | Attributes\.ZendeskTicketId  | 
|  subject  | Title  | 
|  description  | Summary  | 
|  status  | Status  | 
|  requester\_id  | CreatedBy  | 
|  created\_at  | CreatedDate  | 
|  updated\_at  | UpdatedDate  | 

The Zendesk\-tickets customer data from the Zendesk object is associated with a Amazon Connect standard case using the following indexes\. 


| Standard Index Name | Zendesk\-tickets source field | 
| --- | --- | 
|  \_zendeskUserId  | requester\_id  | 
|  \_zendeskTicketId  | id  | 

For example, you can use `_zendeskUserId` and `_zendeskTicketId` as an `ObjectFilter.KeyName` with the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API to find a standard case\. You can find the Zendesk\-tickets objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Zendesk-tickets`\. 