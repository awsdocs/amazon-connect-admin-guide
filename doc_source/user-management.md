# Add users to Amazon Connect<a name="user-management"></a>

You can add users and configure them with permissions that are appropriate to their roles \(for example, agents or managers\)\. For more information, see [Security profiles](connect-security-profiles.md)\. Contacts can be routed based on the skills required of the agents\. For more information, see [Create a routing profile](routing-profiles.md)\.

This topic explains how to add users using the Amazon Connect user interface\. To add users programmatically, see [CreateUser](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateUser.html) in the *Amazon Connect API Reference Guide*\. To use the CLI, see [create\-user](https://docs.aws.amazon.com/cli/latest/reference/connect/create-user.html)\.

## Required permissions for adding users<a name="required-permissions-add-user"></a>

Before you can add users to Amazon Connect, you need the following permissions assigned to your security profile: **Users \- Create**\. The following image shows that this security profile permission is in the **Users and permissions** section of the **Add/Edit security profile** page\. 

![\[The Users and permissions section of the security profile page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/security-profile-create-user-accounts.png)

By default, the Amazon Connect **Admin** security profile has these permissions\.

For information about how add more permissions to an existing security profile, see [Update security profiles](update-security-profiles.md)\.

## Add a user individually<a name="add-a-user"></a>

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\. Use an **Admin** account, or an account assigned to a security profile that has permissions to create users\.

1. In Amazon Connect, on the left navigation menu, choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Create and set up a new user** and then choose **Next**\.

1. Enter the name, email address, secondary email address, mobile number, and password for the user\.

   If you provide a secondary email, the user receives email notifications \- other than password reset notifications \- to this email address instead of to their primary email address\.
**Tip**  
Mobile number is not currently used by Amazon Connect\.

1. Choose a routing profile and a security profile\.

1. Optionally, add resource tags to identify, organize, search for, filter, and control who can access this user\.

1. Choose **Save**\. If the Save button isn't active, it means you're logged in with an Amazon Connect account that doesn't have the required security profile permissions\. 

   To fix this issue, log in with an account that is assigned to the Amazon Connect Admin security profile\. Or, ask another Admin to help\. 

1. For information about adding agents, see [Configure agent settings: routing profile, phone type, and auto\-accept calls](configure-agents.md)\. 

## Add users in bulk from a \.csv file<a name="add-users-in-bulk"></a>

**Note**  
Avoid adding too many unique resources in the \.csv file\. For example, don't add more than 100 different routing profiles\. This may cause a timeout or failure during the validation process\.   
Bulk upload is for adding new records, not for editing existing records\. To edit user records in bulk, see [Edit users in bulk](edit-users-in-bulk.md)\. 

Use these steps to add several users from a \.csv file such as an Excel spreadsheet\.

1. Log in to Amazon Connect with an **Admin** account, or an account assigned to a security profile that has permissions to create users\.

1. In Amazon Connect, on the left navigation menu, choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Upload my users from a template \(\.csv\)** and then choose **Next**\.

   The \.csv template has the following columns in the first row:
   + first name
   + last name
   + email address
   + secondary email address
   + mobile: This is not currently used by Amazon Connect\. 
   + password
   + user login
   + agent hierarchy
   + routing profile name
   + security\_profile\_name\_1\|security\_profile\_name\_2
   + user\_hierarchy\_1\|user\_hierarchy\_2
   + phone type \(soft/desk\)
   + phone number
   + soft phone auto accept yes/no\)
   + ACW timeout \(seconds\)
   + tags

   The following image shows a sample of what the \.csv template looks like in an Excel spreadsheet\. The first row in the spreadsheet contains the column headings, and the second row contains sample user data\.  
![\[The csv template in an Excel spreadsheet.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/add-bulk-users.png)

1. Choose **Download template**\. 

1. Add your users to the template and upload it to Amazon Connect\.

If you get an error message, it usually indicates that one of the required columns is missing information, or there's a typo in one of the cells\. 
+ We recommend checking the format of the phone number as a starting point in your investigation\.
+ If you get an error message that **Security profile is not found**, check whether there's a typo in one of the cells in the **security\_profile\_name\_1** column\.
+ Check that passwords meet requirements: at least 8 characters with an uppercase letter, lowercase letter, and number\. For example, if there's an ellipsis \(\.\.\.\) in a password, this can cause an error\.
+ Update the \.csv file and try uploading it again\.

The following image shows an example error message that you might get when uploading your csv file\. It indicates the routing profile is not valid\.

![\[A sample error message when the csv file is not valid.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/error-message-uploaded-csv-file.png)