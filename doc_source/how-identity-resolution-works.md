# How Identity Resolution works<a name="how-identity-resolution-works"></a>

This topic describes how Identity Resolution performs automatic profile matching, and if set up, how it automatically merges similar profiles\.

## Automatic profile matching<a name="auto-profile-matching"></a>

To identify similar profiles, Identity Resolution uses machine learning to review the following Personal Identifiable Information \(PII\) attributes in each profile: 
+ Name: All names are reviewed for similarity, including first name, middle name, and last name\.
+ Email: All email addresses are reviewed for similarity, including personal email and business email\. They are not case sensitive\.
+ Phone number: All phone numbers and formats are reviewed for similarity, including home phone, mobile phone, and business phone\.
+ Address: All address types and format are reviewed for similarity, including business address, mailing address, shipping address, and billing address\.
+ Date of birth: All birth dates and formats are reviewed for similarity\.

It uses this information to create match groups of similar profiles\. 

### Match groups<a name="match-groups"></a>

A match group consists of all similar profiles which represents a customer\. Each match group contains the following information:
+ A match ID, which uniquely identifies the group of two or more similar profiles that represent a contact
+ The number of profile IDs in the match group
+ A confidence score associated with the match group

### Confidence scores<a name="confidence-score"></a>

After the auto\-matching process runs, you can query the S3 bucket or use the [GetMatches](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetMatches.html) API to filter results based on confidence scores\. For example, you can filter out high confidence matches for a further review\.

A confidence score is a number between 0 and 1 that represents the confidence level of assigning profiles to a match group\. A score of 1 likely indicates an exact match\. 

## Automatic merging of similar profiles<a name="auto-profile-merging"></a>

After the profiles are matched, the Identity Resolution Job can optionally merge similar profiles based on your criteria\. If you delete or update criteria, the updated criteria is applied to similar profiles in the next run\.

**Important**  
You cannot undo the consolidation process\. We strongly recommend using the [GetAutoMergingPreview](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetAutoMergingPreview.html) API to do a dry run of the automatic merging process before running the Identity Resolution Job\.

### How the auto\-merging process works<a name="consolidation-criteria-how-it-works"></a>
+ **All selected attributes in a consolidation criteria are connected with `AND` criteria with exact value comparison before merging**\. 
  + For example, when multiple attributes are specified in the criteria, such as `email address` and `phone number`, then all similar profiles in a match group that have the exact same value of `email address` and `phone number` are merged\.
  + If one or more of the similar profiles in a match group have a different value or missing value for one or more of the attributes in a criteria, the similar profiles are merged\. 

    For example, one match group may be five similar profiles out of which three profiles are consolidated, because these three profiles meet the criteria\. The other two profiles are not merged, because they do not meet the criteria\.
+ **Multiple criteria are evaluated in the order of priority starting with Criteria 1**\. 
  +  The sequence in which consolidation criteria are applied\. It starts with Criteria 1 as the highest priority to Criteria 10 as the lowest priority\. 
  + After the Identity Resolution Job applies one criteria, it applies the next criteria to the consolidated profiles and the remaining similar profiles in a match group\. 
  + You can have a maximum of 10 consolidation criteria\.
+ **Each criteria runs independently and operates as an `OR` with other criteria**\. 
  + When you have multiple criteria, each criteria is applied individually and in the sequence of priority order before the Identity Resolution Job moves on to the next criteria\.
  + All criteria is applied in the sequence in which you listed them\. It doesn't matter whether the criteria fails or succeeds to consolidate similar profiles in a match group\.
+ **By default, profile conflicts are managed by recency**\. 
  + When two or more similar profiles in a match group meet a consolidation criteria, the resulting consolidated profile is created by comparing each value of the profile attributes constituent similar profiles\.
  + Each attribute may have an exact match in value\. In this case, any value may be selected for that attribute\.
  + If there is a conflict between values of two or more constituent similar profiles, the most recently updated attribute is chosen\. 

    For example, if Jane Doe has three different values in the `Address` attribute of the constituent similar profiles, Identity Resolution picks the most recent addressed to create the unified profile\.
  + By default, the **Last updated timestamp** is used to determine the record that was most recently updated\.
+ **Profile conflicts are managed by source object type and recency**\. 
  + You can also change default behavior of conflict resolution to choose a similar constituent profile from a specific source as the source of truth to inform conflict resolution\.
  + If you want to specify a data source to use for profile conflicts, you can choose one of your object types as a data source if you select **Source with last updated timestamp**\. 
  + The most recently updated record from the specified object type is used for resolving profile conflicts\. 
+ **Last updated timestamp identifies which record was most recently updated**\. 
  + The timestamp attribute associated with the source record’s object type is used to identify which record was most recently updated\.
  + If the timestamp attribute is not available for the object type, the timestamp on which the record was ingested into your Customer Profiles domain is used\. 
  + If you have custom object types, you need to add timestamps\. See [Missing timestamp for profile conflicts](create-consolidation-criteria.md#missing-timestamp-for-profile-conflicts) for more information\. 
+ **Consolidation is a one\-way process and cannot be undone**\. 
  + Choose your criteria carefully before starting the consolidation process\. For more information, see [Tips for creating strong criteria](create-consolidation-criteria.md#tips-for-creating-consolidation-criteria)\.
  + Use the [GetAutoMergingPreview](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetAutoMergingPreview.html) API to test the auto\-merging settings of your Identity Resolution without merging your data\. 

For an example that shows how criteria is applied, see [Example: How sample criteria are applied](create-consolidation-criteria.md#criteria-examples)\.