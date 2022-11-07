# Delete/stop Customer Profiles integrations<a name="delete-customer-profile-connection"></a>

**Note**  
Using the Amazon Connect console to delete mapping will only delete objects and data associated with that specific mapping\. If there are multiple objects associated with a profile, then deleting a specific mapping may not clear the profile data\. If you want to delete specific data, then you would delete the mapping, but your profiles may still exist if they contain data from other mappings\. This could result in additional charges for the existing profiles\. The preferred way to delete a domain and all data from Customer Profiles, including all profiles, is to use the [DeleteDomain](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_DeleteDomain.html) API\.

**Console method**

If at any time you want to stop the ingestion of customer profile data, choose the integration/mapping and then choose **Delete**\. 

**API method**
+ To delete customer profiles data for a specific integration, use the `DeleteObjectType` API\.
+ To delete the integrations, customer profiles, and all the customer profile data, use the `DeleteDomain` API\.

To re\-enable the ingestion of customer profile data, go through the setup steps again\. 