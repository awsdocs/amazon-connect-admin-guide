# Use Customer Profiles<a name="customer-profiles"></a>

To help agents deliver more efficient and personalized customer service, Amazon Connect enables you to combine information from external applications, such as Salesforce, with contact history from Amazon Connect\. This creates a customer profile that has all the information agents need during customer interactions in a single place\.

With a single view of customer information and contact history, agents can quickly confirm the customer's identity and determine the reason for the call or chat\. 

Currently, Amazon Connect Customer Profiles can be used in compliance with [GDPR](http://aws.amazon.com/compliance/gdpr-center) and is pending additional certifications held by Amazon Connect\.

The following image shows an agent's Contact Control Panel \(CCP\); for the purposes of this documentation, Amazon Connect Customer Profiles highlighted in the red box\. The agent's application is optimized for multi\-tasking: working on calls, and multiple chats and tasks, with customer profile information in the same browser window\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-concepts-intro3.png)

1. **Product purchase history**: All the assets purchased by a customer can be populated here\. The data is ingested from an external app such as Salesforce or Zendesk that you've [integrated](integrate-external-apps-customer-profiles.md) with Customer Profiles\. 

1. **Contact history**: Date, times, and duration when this customer contacted your contact center in the past\. 

1. **More information**: Information that an agent can use to verify the contact, such as cell phone number and shipping address\. 

1. **Actions**: Agents can copy the contact ID, or choose to go directly to the contact's **Contact record details** page\. 