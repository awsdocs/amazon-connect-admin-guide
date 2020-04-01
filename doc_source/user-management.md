# Add Users<a name="user-management"></a>

You can add users and configure them with permissions that are appropriate to their roles \(for example, agents or managers\)\. For more information, see [Security Profiles](connect-security-profiles.md)\. Contacts can be routed based on the skills required of the agents\. For more information, see [Create a Routing Profile](routing-profiles.md)\.

## Add a user individually<a name="add-a-user"></a>

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create users\.

1. Choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Create and set up a new user** and then choose **Next**\.

1. Enter the name, email address, and password for the user\.

1. Choose a routing profile and a security profile\.

1. Choose **Save**\. If the Save button isn't active, it means you don't have permissions to add or edit a user\. 

## Add users in bulk<a name="add-users-in-bulk"></a>

Use these steps to add several users from an Excel spreadsheet \(\.csv\)

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create users\.

1. Choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Upload my users from a template \(csv\)** and then choose **Next**\.

1. Choose **Download template**\. 

1. Add your users to the template and upload it to Amazon Connect\.

If you get an error message usually indicates that one of the required columns is missing information, or there's a typo in one of the cells\. Update the \.csv file and try uploading it again\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/error-message-uploaded-csv-file.png)