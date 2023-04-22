# Update security profiles<a name="update-security-profiles"></a>

You can update a security profile at any time to add or remove permissions\.

## Required permissions to update security profiles<a name="update-security-profiles-required-permissions"></a>

Before you can update permissions in a security profile, you must be logged in with an Amazon Connect account that has the following permissions: **Security profiles \- Edit**\. 

![\[The users and permissions section of the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/security-profile-edit.png)

By default, the Amazon Connect **Admin** security profile has these permissions\.

## How to update security profiles<a name="how-to-update-security-profiles"></a>

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\. You must be logged in with an Amazon Connect account that has permissions to update security profiles\.

1. Choose **Users**, **Security profiles**\.

1. Select the name of the profile\.

1. Update the name, description, permissions, access control, and resource tags as needed\.

1. Choose **Save**\.

**Note**  
Modifying the access control or resource tags on a security profile may impact the features or resources that a user with this security profile can access\.