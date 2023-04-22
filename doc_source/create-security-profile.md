# Create a security profile<a name="create-security-profile"></a>

Creating a security profile enables you to grant your users only the permissions that they need\.

For each permission group, there is a set of resources and supported set of actions\. For example, users are part of the **Users and permissions** group, which supports the following actions: view, edit, create, remove, enable/disable, and edit permission\. 

Some actions depend on other actions\. When you choose an action that depends on another action, the dependent action is automatically chosen and must also be granted\. For example, if you add permission to edit users, we also add permission to view users\.

## Required permissions to create security profiles<a name="create-security-profiles-required-permissions"></a>

Before you can create a new security profile, you must be logged in with an Amazon Connect account that has **Security profiles \- Create** permissions, as shown in the following image\. 

![\[The users and permissions section of the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/security-profile-create.png)

By default, the Amazon Connect **Admin** security profile has these permissions\.

## How to create security profiles<a name="how-to-security-profiles-required-permissions"></a>

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\.

1. Choose **Users**, **Security profiles**\.

1. Choose **Add new security profile**\.

1. Type a name and description for the security profile\.

1. Choose the appropriate permissions for the security profile from each permission group\. For each permission type, choose one or more actions\. Selecting some actions results in other actions being selected\. For example, selecting **Edit** also selects **View** for the resource and any dependent resources\.

1. Choose **Save**\.

## Tag\-based access controls<a name="security-profile-tag-based-access-controls"></a>

You create a security profile with access control tags\. Use these steps to create a security profile that enforces tag\-based access controls\.

1. Choose **Show advanced settings** at the bottom of the security profile\.

1. In the **Access control** section, in the **Resources** box, enter the resources to be restricted using tags\.  
![\[The access control section of the security profile page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tag-access-control-sp.png)

1. Enter the **Key** and **Value** combination for the resource tags that you want to restrict access to\.

1. Ensure that you have enabled *View* permissions for the resources that you have selected\.

1. Choose **Save**\.

**Note**  
It is mandatory to specify both a resource type and an access control tag when configuring tag based access controls\. As a best practice, ensure that you have matching resource tags on a security profile that has tag based access controls configured\. To learn more about tag based access controls in Amazon Connect, see [Tag\-based access control](tag-based-access-control.md)\.

## Tag security profiles<a name="security-profile-tagging"></a>

You can create a new security profile with resource tags\. Use these steps to add a resource tag to a security profile\.

1. Choose **Show advanced settings** at the bottom of the security profile\.

1. Enter a **Key** and **Value** combination to tag the resource, as shown in the following image\.  
![\[The tags section of the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tag-securit-profiles-sp.png)

1. Choose **Save**\.

For more information about tagging resources, see [Tagging resources in Amazon Connect](tagging.md)\.