# Edit users in bulk<a name="edit-users-in-bulk"></a>

This topic explains how to edit user records using the Amazon Connect user interface\. To edit user records programmatically, see [UpdateUserIdentityInfo](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateUserIdentityInfo.html) in the *Amazon Connect API Reference Guide*\. To use the CLI, see [update\-user\-identity\-info](https://docs.aws.amazon.com/cli/latest/reference/connect/update-user-identity-info.html)\.

1. Log in to Amazon Connect with an Admin account, or an account assigned to a security profile that has permissions to edit user accounts\.

1. In Amazon Connect, on the left navigation menu, choose **Users**, **User management**\. 

1. To edit all the records on the page, choose the top box\. Otherwise, select one or more records you want to edit at the same time\. Choose **Edit**\.  
![\[The User management page, with an arrow pointing to the top box, which selects all the user records on the page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/user-management-edit-select.png)

1. On the **Bulk edit** page, in the **Settings** section, you can choose the following settings for all of the selected users:
   + Security profile
   + Routing profile
   + Phone type
   + After Call Work \(ACW\) timeout
   + Agent hierarchy, if this has been set up
   + Tags

1. Choose **Save** to apply your changes to the selected records\.