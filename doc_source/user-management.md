# Add users to Amazon Connect<a name="user-management"></a>

You can add users and configure them with permissions that are appropriate to their roles \(for example, agents or managers\)\. For more information, see [Security profiles](connect-security-profiles.md)\. Contacts can be routed based on the skills required of the agents\. For more information, see [Create a routing profile](routing-profiles.md)\.

## Required permissions for adding users<a name="required-permissions-add-user"></a>

Before you can add users to Amazon Connect, you need the following permissions assigned to your security profile: **Users \- Create**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/security-profile-create-user-accounts.png)

By default, the Amazon Connect **Admin** security profile has these permissions\.

For information about how add more permissions to an existing security profile, see [Update security profiles](update-security-profiles.md)\.

## Add a user individually<a name="add-a-user"></a>

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create users\.

1. Choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Create and set up a new user** and then choose **Next**\.

1. Enter the name, email address, secondary email address, mobile number, and password for the user\.

   If you provide a secondary email, the user receives email notifications \- other than password reset notifications \- to this email address instead of to their primary email address\.

1. Choose a routing profile and a security profile\.

1. Choose **Save**\. If the Save button isn't active, it means you're logged in with an Amazon Connect account that doesn't have the required security profile permissions\. 

   To fix this issue, log in with an account that is assigned to the Amazon Connect Admin security profile\. Or, ask another Admin to help\. 

1. For information about adding agents, see [Configure agent settings: routing profile, phone type, and auto\-accept calls](configure-agents.md)\. 

## Add users in bulk from a \.csv file<a name="add-users-in-bulk"></a>

Use these steps to add several users from a \.csv file such as an Excel spreadsheet\.

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create users\.

1. Choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Upload my users from a template \(\.csv\)** and then choose **Next**\.

   The \.csv template has the following columns in the first row:
   + first name
   + last name
   + email address
   + secondary email address
   + mobile
   + password
   + user login
   + routing profile name
   + security\_profile\_name\_1\|security\_profile\_name\_2
   + phone type \(soft/desk\)
   + phone number
   + soft phone auto accept yes/no\)
   + ACW timeout \(seconds\)

   The following image shows a sample of what the \.csv template looks like in an Excel spreadsheet:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/add-bulk-users.png)

1. Choose **Download template**\. 

1. Add your users to the template and upload it to Amazon Connect\.

If you get an error message, it usually indicates that one of the required columns is missing information, or there's a typo in one of the cells\. 
+ We recommend checking the format of the phone number as a starting point in your investigation\.
+ If you get an error message that **Security profile is not found**, check whether there's a typo in one of the cells in the **security\_profile\_name\_1** column\.
+ Update the \.csv file and try uploading it again\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/error-message-uploaded-csv-file.png)