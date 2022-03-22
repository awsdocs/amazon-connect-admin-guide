# Integrate external applications with Customer Profiles<a name="integrate-external-apps-customer-profiles"></a>

Amazon Connect provides a set of pre\-built integrations powered by Amazon AppFlow and Amazon EventBridge\. After you enable Amazon Connect Customer Profiles, you can use these integrations to combine information from external applications such as Salesforce or Zendesk, with contact history from Amazon Connect\. This creates a customer profile that has all the information agents need during customer interactions in a single place\.

You can also use Customer Profiles in Amazon AppFlow\. Amazon AppFlow supports `CustomerProfiles` as a destination\. You can use Amazon AppFlow APIs to send data into Customer Profiles using `CustomerProfiles` as the destination name\.

Before you begin, make sure you are using a customer managed key\. For more information about configuring KMS keys, see [Create a KMS key to be used by Customer Profiles to encrypt data \(required\)](enable-customer-profiles.md#enable-customer-profiles-awsmanagedkey)\. 

**Topics**
+ [Set up integration for Salesforce, ServiceNow, Marketo, or Zendesk](integrate-customer-profiles-appflow.md)
+ [Set up integration for Segment](integrate-customer-profiles-segment.md)
+ [Set up integration for Shopify](integrate-customer-profiles-shopify.md)
+ [Delete/stop Customer Profiles integrations](delete-customer-profile-connection.md)