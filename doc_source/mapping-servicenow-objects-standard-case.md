# Mapping ServiceNow objects to the standard case<a name="mapping-servicenow-objects-standard-case"></a>

This topic lists which fields in ServiceNow objects map to fields in the standard case in Amazon Connect Customer Profiles\.

## Servicenow\-task object<a name="servicenow-task-object"></a>

Following is list of all the fields in a Servicenow\-task object\. 
+ sys\_id
+ active
+ activity\_due
+ additional\_assignee\_list
+ approval
+ approval\_history
+ approval\_set
+ assigned\_to
+ assignment\_group
+ business\_duration
+ business\_service
+ calendar\_duration
+ closed\_at
+ closed\_by
+ cmdb\_ci\.display\_value
+ cmdb\_ci\.link
+ comments
+ comments\_and\_work\_notes
+ company
+ contact\_type
+ contract
+ correlation\_display
+ active
+ correlation\_id
+ delivery\_plan
+ delivery\_task
+ description
+ due\_date
+ escalation
+ expected\_start
+ follow\_up
+ group\_list
+ impact
+ knowledge
+ location
+ made\_sla
+ number
+ opened\_at
+ opened\_by\.display\_value
+ order
+ parent
+ priority
+ reassignment\_count
+ service\_offering
+ short\_description
+ sla\_due
+ state
+ sys\_class\_name
+ sys\_created\_by
+ sys\_created\_on
+ active
+ sys\_domain\.global
+ sys\_domain\.link
+ sys\_domain\_path
+ sys\_mod\_count
+ sys\_updated\_by
+ sys\_updated\_on
+ time\_worked
+ upon\_approval
+ upon\_reject
+ urgency
+ user\_input
+ watch\_list
+ work\_end
+ work\_notes
+ work\_notes\_list
+ work\_start

## Mapping Servicenow\-task to a standard case<a name="mapping-servicenow-task-case"></a>

A subset of the fields in the Servicenow\-task object map to the standard case in Customer Profiles\. 

The following table lists which fields can be mapped from the Servicenow\-task object to the standard case\. 


| Servicenow\-task source field | Standard case target field | 
| --- | --- | 
|  sys\_id  | Attributes\.ServiceNowTaskId  | 
|  opened\_by\.link  | Attributes\.ServiceNowSystemUserId  | 
|  short\_description  | Title  | 
|  description  | Summary  | 
|  status  | Status  | 
|  sys\_created\_by  | CreatedBy  | 
|  sys\_created\_on  | CreatedDate  | 
|  sys\_updated\_on  | UpdatedDate  | 

The Servicenow\-task customer data from Servicenow is associated with an Amazon Connect standard case using the indexes in the following table\. 


| Standard Index Name | Servicenow\-task source field | 
| --- | --- | 
|  \_serviceNowTaskId  | sys\_id  | 
|  \_serviceNowSystemId  | open\_by\.link  | 

For example, you can use `_serviceNowTaskId` and `_serviceNowSystemId` as an `ObjectFilter.KeyName` with the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API to find a standard case\. You can find the Servicenow\-task objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Servicenow-task`\.

## Servicenow\-incident object<a name="servicenowincident-object"></a>

Following is a list of all the fields in a Servicenow\-incident object\. 
+ sys\_id
+ business\_stc
+ calendar\_stc
+ caller\_id\.link
+ caller\_id\.value
+ category
+ caused\_by
+ child\_incidents
+ close\_code
+ hold\_reason
+ incident\_state
+ notify
+ parent\_incident
+ problem\_id
+ reopened\_by
+ reopened\_time
+ reopen\_count
+ resolved\_at
+ resolved\_by\.link
+ resolved\_by\.value
+ rfc
+ severity
+ subcategory

## Mapping Servicenow\-incident to a standard case<a name="mapping-servicenowincident-case"></a>

A subset of the fields in the Servicenow\-incident object map to the standard case in Customer Profiles\.

The following table lists which fields can be mapped from the Servicenow\-incident object to the standard case\. 


| Servicenow\-Incident source field | Standard case target field | 
| --- | --- | 
| sys\_id  |  Attributes\_ServiceNowIncidentId  | 
| caller\_id\.link  |  Attributes\_ServiceNowSystemUserId  | 
| incident\_status  |  Status  | 
| caller\_id\.link  |  CreatedBy  | 
| resolved\_at  |  ClosedDate  | 
| category  |  Reason  | 

The Servicenow\-incident customer data from the Servicenow object is associated with an Amazon Connect standard case using the indexes in the following table\. 


| Standard Index Name | Servicenow source field | 
| --- | --- | 
| \_serviceNowIncidentId  |  sys\_id  | 
| \_serviceNowSystemId  |  caller\_id\.link  | 

For example, you can use `_serviceNowIncidentId` and `_serviceNowSystemId` as a ObjectFilter\.KeyName with the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API to find a standard case\. You can find the Servicenow\-incident objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Servicenow-incident`\.