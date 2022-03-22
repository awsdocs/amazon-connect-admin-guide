# Set up consolidation criteria for Identity Resolution<a name="create-consolidation-criteria"></a>

**Note**  
You must [enable Identity Resolution](#create-consolidation-criteria) in order to access the option to create consolidation criteria using the Amazon Connect admin console\. 

When similar profiles are detected by an Identity Resolution Job, the process can automatically merge them into a unified profile based on consolidation criteria that you specify\. 

The attributes that you select are compared across all similar profiles in a match group for exact match\. For example, if you specify `email` as an attribute in the criteria, then all similar profiles in a match group that have exact same value of `email address` are merged into a unified profile\. 

**Tip**  
If you want to set up your own merging logic, use the [MergeProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_MergeProfiles.html) API\.

## Limits<a name="criteria-limitations"></a>

You can select any attribute from the [standard profile](standard-profile-definition.md) to compare similar profiles\. For example, you might choose phone number, email address, and name, as well as custom attributes\. 

You can specify up to: 
+ 10 consolidation criteria
+  20 attributes per criteria

## Tips for creating strong criteria<a name="tips-for-creating-consolidation-criteria"></a>

To improve the targeting of unique profiles and to avoid consolidating profiles that are not duplicates, we recommend the following steps:
+ Select attributes that can uniquely identify a customer and are not likely to be the same across customers, such as an account number or a form of government ID\.
+ Avoid single attribute criteria\. Select multiple attributes to create a combination of attributes to improve targeting\. For example:
  + **Phone number** with **First name**, **Middle name**, **Last name** is stronger criteria

  than
  + **Phone number** alone, or 
  + The combination of **First name, Middle, name, Last name** alone
+ Select all attributes within a specific attribute group, when applicable\. For example, if you want to use name, select all the related name attributes: **First name, Middle name, Last name**\. If you want to use business address, select all the related business address attributes\. 
+ Include one of the following attributes likely to uniquely identify a customer in combination with other attributes in the criteria:
  + Account number
  + Phone number
  + Email

## How to set up automerging criteria<a name="howto-setup-automerging-criteria"></a>

Before setting up your consolidation criteria for automatic merging, or automerging, we recommend reviewing [How the auto\-merging process works](how-identity-resolution-works.md#consolidation-criteria-how-it-works)\.

1. After you enable Identity Resolution, on the **Identity Resolution** page you'll have the option of setting up auto\-merging criteria\. Choose **Create consolidation criteria**\.

1. If you receive a **Missing timestamp** dialog box, we recommend adding new timestamp attributes to your custom object types before continuing\. See [Missing timestamp for profile conflicts](#missing-timestamp-for-profile-conflicts)\. 

1. In the **Profile conflicts** section, choose how profile conflicts should be resolved when two or more records have conflicts\.

1. In the **Consolidation criteria** section, create one or more criteria\. We recommend including at least two or more attributes per criteria\.

## Missing timestamp for profile conflicts<a name="missing-timestamp-for-profile-conflicts"></a>

The **Missing timestamp** message is displayed if you have custom object type mappings\.

Use the [PutProfileObjectType](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutProfileObjectType.html) API to add the following new attributes to your custom object type: 
+ `sourceLastUpdatedTimestamp`
+ `sourceLastUpdatedTimestampFormat`

If the timestamp attribute is not specified, you can continue to create consolidation criteria, however, a default timestamp of when the records were ingested into Customer Profiles is used\. We recommend adding the new attributes before creating your consolidation criteria\.

If you have already defined a custom object type and want to update your custom object type, we run a scheduled backfill every week to update your existing profiles with the `sourceLastUpdatedTimestamp`\. To opt in to the scheduled backfill:

1. Update your custom profile object type by using the [PutProfileObjectType](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutProfileObjectType.html) API\.

1. After you update your custom profile object type, open an [AWS Support ticket](https://console.aws.amazon.com/support/home) and we’ll schedule the backfill for you\. The scheduled backfill runs until end of February 2022\.

Alternatively, you can delete and then re\-create the ingestion/connector you have for your domain that uses the custom object type\. All of your data will be re\-ingested using your updated object type and `sourceLastUpdatedTimestamp` will be parsed from it\.

## Example: How sample criteria are applied<a name="criteria-examples"></a>

In this example there are three criteria: 
+ **Resolve profile conflicts** is set to **Use last updated timestamp**\. This means when two fields have conflicting values, Identity Resolution is going to use the last updated timestamp to determine which value to use\.
+ Criteria 1: 
  + First name, Last name
  + Email
+ Criteria 2: 
  + Phone number

These criteria are applied to the following profiles:
+ Profile A
  + John Doe \[last updated **05:00**a\]
  + doefamily@anyemail\.com \[last updated **05:00**a\]
  + 555\-555\-5555 \[last updated **07:00**a\]
+ Profile B
  + John Doe \[last updated **04:00**a\]
  + doefamily@anyemail\.com \[last updated **06:00**a\]
  + 555\-555\-555**6** \[last updated *04:00*a\]
+ Profile C
  + **Jane** Doe \[last updated **06:00**a\]
  + doefamily@anyemail\.com \[last updated **07:00**a\]
  + 555\-555\-5555 \[last updated **06:00**a\]

Following are the results when Criteria 1 is applied:
+ Profile A and B are merged = Profile AB

This results in ProfileAB, which looks like the following:
+ John Doe \[last updated **05:00**a\]
+ doefamily@anyemail\.com \[last updated **07:00**a\]
+ 555\-555\-555**5** \[last updated **06:00**a\]

Because there's a conflict between the phone numbers, Identity Resolution uses the last timestamp to choose the 555\-555\-555 number\.

Next, Criteria 2 is applied\. Following are the results:
+ Profile AB and C are merged = Profile ABC

This results in ProfileABC, which looks like the following:
+ **Jane** Doe \[last updated **06:00**a\]
+ doefamily@anyemail\.com \[last updated **07:00**a\]
+ 555\-555\-555**5** \[last updated **07:00**a\]

Identity Resolution uses the First name, Last name, and Email from Profile C because they have the most recent timestamps\. 