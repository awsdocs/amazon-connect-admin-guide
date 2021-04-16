# Best practices for security profiles<a name="security-profile-best-practices"></a>
+ Limit who has **Users \- Edit or Create** permissions

  People with these permissions pose a risk to your contact center because they can do the following:
  + Reset passwords, including that of the administrator\.
  + Change the login credentials of a user, including the login username\.
  + Grant other users permission to the Admin security profile\. People assigned to the Admin security profile have full access to your contact center\.

  Doing these things would enable someone to lock out those who need to access Amazon Connect, and allow in others who can steal customer data and damage your business\. 

  To reduce the risk, as a best practice we recommend limiting the number of people who have **Users \- Edit or Create** permissions\.
+ [Use AWS CloudTrail](logging-using-cloudtrail.md) to log the requests and responses of [UpdateUserIdentityInfo](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserIdentityInfo.html)\. This enables you to track changes made to user information\. Someone who has the ability to call the `UpdateUserIdentityInfo` API can change a user's email address to one owned by an attacker, and then reset the password through email\. 
+ [Understand inherited permissions](inherited-permissions.md)

  Some security profiles included inherited permissions: when you assign dedicated permissions to one object, by default permissions are granted to sub\-objects\. For example, when you grant dedicated permission to edit users, you also grant them permission to list all security profiles for your Amazon Connect instance\. This because to edit users, the person has access to drop\-down list of security profiles\. 

  Before assigning security profiles, review the list of inherited permissions\.
+ [Track who accesses recordings](track-who-deleted-recordings.md)\.

   In the **Metrics and quality** permission group, you can enable a download icon for recorded conversations\. When members of this group go to **Metrics and quality**, **Contact search**, and then search contacts, they will see an icon to download recordings\. 
**Important**  
This setting isn't a security feature\. **Users who don't have this permission can still download recordings using other less\-discoverable ways**\.

  We recommend that you track who in your organization accesses recordings\.