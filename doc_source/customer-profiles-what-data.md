# What is a customer profile?<a name="customer-profiles-what-data"></a>

A customer profile contains contact history and values for the standard profile attributes\. The standard profile attributes are, for example, account number, address, billing address, and birth date\.

After you enable Amazon Connect Customer Profiles, you can [ingest data from external applications](integrate-external-apps-customer-profiles.md) into the customer profiles\. 

You can also add custom fields and objects to the customer profiles by using the [Amazon Connect Customer Profiles APIs](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/Welcome.html)\.

## Where is customer profile data stored?<a name="customer-profiles-data-storage"></a>

Amazon Connect creates and stores a unique customer profile for every contact\. It parses the external application data, and stores it as customer profile attributes\. 

Amazon Connect does not replace or update the data in the external application\. If a data source is removed, the data from the external application is no longer available in the customer profile\. 

For information about how customer profile data are secured, see [Data protection in Amazon Connect](data-protection.md)\.