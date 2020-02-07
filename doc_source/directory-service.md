# Use an Existing Directory for Identity Management<a name="directory-service"></a>

If you are already using a AWS Directory Service directory to manage users, you can use the same directory to manage user accounts in Amazon Connect\. You can also create a new directory in AWS Directory Service to use for Amazon Connect\. The directory you choose must be associated with your AWS account, and must be active in the AWS Region in which you create your instance\. You can associate an AWS Directory Service directory with only one Amazon Connect instance at a time\. To use the directory with a different instance, you must delete the instance with which it is already associated\.

The following AWS Directory Service directories are supported in Amazon Connect:
+ [Microsoft Active Directory](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_microsoft_ad.html)—AWS Directory Service lets you run Microsoft Active Directory as a managed service\.
+ [Active Directory Connector](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_ad_connector.html)—AD Connector is a directory gateway you can use to redirect directory requests to your on\-premises Microsoft Active Directory\. 
+ [Simple Active Directory](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_simple_ad.html)—Simple AD is a standalone managed directory that is powered by a Samba 4 Active Directory compatible server\.

You cannot change the identity option you select after you create the instance\. If you decide to change the directory you selected, you can delete the instance and create a new one\. When you delete an instance, you lose all configuration settings and metrics data for it\.

There is no additional charge for using an existing or a proprietary directory in Amazon Connect\. For information about the costs associated with using AWS Directory Service, see [AWS Service Pricing Overview](http://aws.amazon.compricing)\.

The following limitations apply to all new directories created using AWS Directory Service:
+ Directories can only have alphanumeric names\. Only the '\.' character can be used\.
+ Directories cannot be unbound from an Amazon Connect instance after they have been associated\.
+ Only one directory can be added to an Amazon Connect instance\.
+ Directories cannot be shared across multiple Amazon Connect instances\.