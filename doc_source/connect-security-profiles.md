# Amazon Connect Security Profiles<a name="connect-security-profiles"></a>

Security profiles consist of permissions that determine which Amazon Connect users can view, update, or create which Amazon Connect resources or perform specific tasks\. Assigning a security profile to a user grants that user the permissions you added to the security profile\. For example, you can grant users read/write access to routing profiles\.

Security profiles are organized into the following permission groups:
+ **Routing**—Grant access to routing profiles, quick connects, hours of operation, and queues\.
+ **Numbers and flows**—Grant access to prompts, contact flows, and phone numbers\.
+ **Users and permissions**—Grant access to users, agent hierarchies, security profiles, and agent status\.
+ **Contact Control Panel \(CCP\)**—Grant access to the CCP and to make outbound calls\.
+ **Metrics and Quality**—Grant access to metrics, contact search, contact attributes, login/logout reports, manager listen in, call recordings, and saved reports\.
+ **Historical Changes**—Grant access to view historical changes\.

For each permission group, there is a set of resources and supported set of actions\. For example, users are part of the **Users and permissions** group, which supports the following actions: view, edit, create, remove, enable/disable, and edit permission\. Some actions depend on other actions\. When you choose an action that depends on another action, the dependent action is automatically chosen and must also be granted\. For example, if you add permission to edit users, we also add permission to view users\.

## Considerations<a name="considerations"></a>
+ When you grant permission to edit users, you also grant permission to reset user passwords, including that of the administrator\.
+ When you grant permission to create or edit users, you also grant permission to assign users a security profile that grants them full access to the contact center\.
+ In the Metrics and Quality permission group, you can enable a download icon for recorded conversations\. When members of this group go to **Metrics and quality**, **Contact search**, and then do a search of calls, they will see an icon to download recordings\. 
**Important**  
This setting isn't a security feature\. Users who don't have this permission can still download recordings using other less\-discoverable ways\.

## Default Security Profiles<a name="default-security-profiles"></a>

We provide default security profiles for general roles\. You can review the permissions granted by these profiles and use them if they align with the permissions that your users need\. Otherwise, create a security profile that grants your users only the permissions they need\.

The following are the default security profiles:
+ **Admin**—Grants administrators permission to perform all actions\.
+ **Agent**—Grants agents permission to access the CCP\.
+ **CallCenterManager**—Grants managers permission to perform actions related to user management, metrics, and routing\.
+ **QualityAnalyst**—Grants analysts permission to perform actions related to metrics\.

## Create a Security Profile<a name="create-security-profile"></a>

Creating a security profile enables you to grant your users only the permissions that they need\.

**To create a security profile**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Users**, **Security profiles**\.

1. Choose **Add new security profile**\.

1. Type a name and description for the security profile\.

1. Choose the appropriate permissions for the security profile from each permission group\. For each permission type, choose one or more actions\. Selecting some actions results in other actions being selected\. For example, selecting **Edit** also selects **View** for the resource and any dependent resources\.

1. Choose **Save**\.

## Update Security Profiles<a name="update-security-profiles"></a>

You can update a security profile at any time\.

**To update security profiles**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Users**, **Security profiles**\.

1. Select the name of the profile\.

1. Update the name, description, and permissions as needed\.

1. Choose **Save**\.

## Assign a Security Profile to a User<a name="assign-security-profile"></a>

**To assign a security profile to a user**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Users**, **User management**\.

1. Select one or more users and choose **Edit**\.

1. For **Security Profiles**, add or remove security profiles as needed\. To add a security profile, put your cursor in the field and select the security profile from the list\. To remove a security profile, click the **x** next to its name\. 

1. Choose **Save**\.