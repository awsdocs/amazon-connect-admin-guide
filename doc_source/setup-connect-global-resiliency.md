# Set up Amazon Connect Global Resiliency<a name="setup-connect-global-resiliency"></a>

**Note**  
This feature is available only for Amazon Connect instances created in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.   
To obtain access to this feature, contact your Amazon Connect Solutions Architect or Technical Account Manager\.

Amazon Connect Global Resiliency enables you to provide customer service anywhere in the world with the highest reliability, performance, and efficiency\. With its distributed telephony features, your contact center can meet international regulatory requirements\. 

Amazon Connect Global Resiliency provides a set of APIs that you use to:
+ Provision a linked Amazon Connect instance in another AWS Region\.
+ Provision and manage phone numbers that are global and accessible in both Regions\.
+ Distribute telephony traffic between the instances and across Regions in 10% increments\. 

  For example, you can distribute traffic 100% in US East \(N\. Virginia\) / 0% in US West \(Oregon\), or 50% in each Region\.
+ Access reserved capacity across Regions\.

**Topics**
+ [Get started](get-started-connect-global-resiliency.md)
+ [Manage traffic distribution groups](manage-traffic-distribution-groups.md)
+ [Manage phone numbers across Regions](manage-phone-numbers-across-regions.md)