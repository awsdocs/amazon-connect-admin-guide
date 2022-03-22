# Delete users from your Amazon Connect instance<a name="delete-users"></a>

When a user is deleted from Amazon Connect, you won't be able to configure their agent settings any more\. For example, you won't be able to assign a routing profile to them\.

## What happens to the user's metrics?<a name="delete-users-metrics"></a>

The user's data in contact records and reports is retained\. The data is preserved for the consistency of the historical metrics\.

In the historical metrics reports, the agent's data will be included in the **Agent performance** metrics report\. However, you won't be able to see an **Agent activity audit** of the deleted agent because their name won't appear in the drop\-down list\. 

## Required permissions to delete users<a name="required-permissions-delete-users"></a>

Before you can update permissions in a security profile, you must be logged in with an Amazon Connect account that has the following permissions: **Users \- Remove**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/delete-users-required-permissions.png)

By default, the Amazon Connect **Admin** security profile has these permissions\.

## How to delete users<a name="how-to-delete-users"></a>

You can't undo a deletion\.

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to remove users\.

1. Choose the user account you want to delete, and then choose **Remove**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/delete-users-how-to.png)

1. Confirm you want to delete that account\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/delete-users-confirm.png)

1. Note the status of account\. Choose **Back** to return to the **User management** page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/delete-users-confirm-back.png)