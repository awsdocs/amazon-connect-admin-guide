# Download user accounts from your Amazon Connect instance<a name="download-user-records"></a>

You can export a list of user accounts from Amazon Connect to a \.csv file\. The output is limited to the results that appear on the page; it does not include all the accounts, if you have more users than appear on the page\.

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\. Use an **Admin** account, or an account assigned to a security profile that has **Users and permissions \- Users \- Edit** permissions\.

1. In Amazon Connect, on the left navigation menu, choose **Users**, **User management**\.

1. Choose **Download CSV**\.
**Tip**  
If a user has **Users \- View permissions** instead of **Edit** permissions, they will see the **Download CSV** option on their page, but when they choose it, the \.csv file will be empty\.