# Use Customer Profiles in the agent application<a name="use-customer-profiles"></a>

To help you deliver more efficient and personalized customer service, Amazon Connect enables you to combine information from external applications, such as Salesforce, with contact history from Amazon Connect\. This creates a customer profile that has all the information you need during customer interactions in a single place\.

The following image shows an agent's Contact Control Panel \(CCP\); for the purposes of this documentation, Amazon Connect Customer Profiles is highlighted in the red box\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-concepts-intro3.png)

1. **Product purchase history**: All the assets purchased by a customer can be populated here\. The data is ingested from an external app such as Salesforce or Zendesk that you've [integrated](integrate-external-apps-customer-profiles.md) with Customer Profiles\. 

1. **Contact history**: Date, times, and duration when this customer contacted your contact center in the past\. 

1. **More information**: Information that an agent can use to verify the contact, such as cell phone number and shipping address\. 

1. **Actions**: Agents can copy the contact ID, or choose to go directly to the contact's **Contact record details** page\. 

**Topics**
+ [Accept incoming contacts with Customer Profiles](select-customer-profile.md)
+ [Create a new customer profile](create-new-customer-profile.md)
+ [Search for a customer profile](search-customer-profile.md)