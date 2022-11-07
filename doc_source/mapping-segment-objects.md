# Mapping Segment objects to the standard profile object<a name="mapping-segment-objects"></a>

This topic lists which fields in Segment objects map to fields in the standard profile object in Amazon Connect Customer Profiles\.

## Segment\-Identify object<a name="segment-identify-object"></a>

Following is a list of all the fields in a Segment\-Identify object\.
+ userId
+ common fields \- see [Spec: Common Fields](https://segment.com/docs/connections/spec/common/) in the Segment documentation
+ Segment reserved traits \- see [Traits](https://segment.com/docs/connections/spec/identify/#traits) in the Segment documentation
+ traits\.address\.street 
+ traits\.address\.city
+ traits\.address\.state
+ traits\.address\.postalCode
+ traits\.address\.country
+ traits\.age
+ traits\.avatar
+ traits\.birthday
+ traits\.company\.name
+ traits\.company\.id
+ traits\.company\.industry
+ traits\.company\.employee\_count
+ traits\.company\.plan
+ traits\.createdAt
+ traits\.description
+ traits\.email
+ traits\.firstName
+ traits\.gender
+ traits\.id
+ traits\.lastName
+ traits\.name
+ traits\.phone
+ traits\.title
+ traits\.username
+ traits\.website

## Mapping a Segment\-Identify to a standard profile object<a name="mapping-segment-identify-object"></a>

A subset of the fields in the Segment\-Identify object map to the standard profile object in Customer Profiles\. 

The following table lists which fields can be mapped from the Segment\-Identify object to the standard profile\.


|  |  | 
| --- |--- |
| Segment\-Identify source field | Standard profile target field | 
| userId | Attributes\.SegmentUserId | 
| traits\.company\.name | BusinessName | 
| traits\.firstName | FirstName | 
| traits\.lastName | LastName | 
| traits\.birthday | BirthDate | 
| traits\.gender | Gender | 
| traits\.phone | PhoneNumber | 
| traits\.email | EmailAddress | 
| traits\.address\.street | Address\.Address1 | 
| traits\.address\.city | Address\.City | 
| traits\.address\.state | Address\.State | 
| traits\.address\.country | Address\.Country | 
| traits\.address\.postalCode | Address\.PostalCode | 

### Example<a name="example-mapping-segment-identify-object"></a>

The following example shows how to map a source field to a target field\.

```
"segmentUserId": {
    "Source": "_source.detail.event.detail.userId",
    "Target": "_profile.Attributes.SegmentUserId"
}
```

The Segment\-Identify customer data from the Segment object is associated with an Amazon Connect customer profile using the following index\. 


| Standard Index Name | Segment\-Identify source field | 
| --- | --- | 
|  \_segmentUserId  |  userId  | 

For example, you can use `_segmentUserId` as a key name with the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to find an Amazon Connect customer profile\. You can find the Segment\-Identify objects associated with a specific profile by using the [ListProfileObjects](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_ListProfileObjects.html) API with the `ProfileId` and `ObjectTypeName` set to `Segment-Identify`\.