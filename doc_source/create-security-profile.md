# Create a security profile<a name="create-security-profile"></a>

Creating a security profile enables you to grant your users only the permissions that they need\.

For each permission group, there is a set of resources and supported set of actions\. For example, users are part of the **Users and permissions** group, which supports the following actions: view, edit, create, remove, enable/disable, and edit permission\. 

Some actions depend on other actions\. When you choose an action that depends on another action, the dependent action is automatically chosen and must also be granted\. For example, if you add permission to edit users, we also add permission to view users\.

**To create a security profile**

1. Log in to your contact center using your access URL \(https://*instance name*\.awsapps\.com/connect/login\)\.

1. Choose **Users**, **Security profiles**\.

1. Choose **Add new security profile**\.

1. Type a name and description for the security profile\.

1. Choose the appropriate permissions for the security profile from each permission group\. For each permission type, choose one or more actions\. Selecting some actions results in other actions being selected\. For example, selecting **Edit** also selects **View** for the resource and any dependent resources\.

1. Choose **Save**\.