# Security profile permissions for Cases<a name="assign-security-profile-cases"></a>

The following image shows the security permissions used to manage access to [Amazon Connect Cases](cases.md) functionality:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-security-profile-permissions.png)

Also, to use Amazon Connect Cases, your users also need permissions to Customer Profiles permissions\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-customer-profiles-permissions.png)

Assign the following permissions to manage who can create, view, and edit cases, case fields, and case templates:
+ **Cases**: Manage who can access cases by using the agent application\.
  + **View case**: Allows the user to view and search cases in the agent application\. This includes viewing case data \(for example, status, title, summary\), contact history \(for example, calls, chats, tasks with information such as start time, end time, duration, etc\.\), and comments\.
  + **Edit case**: Allows the user to edit cases, which includes editing case data \(for example, update case status\), add comments, and associate contacts to cases\.
  + **Create case**: Allows the user to create new cases, and associate contacts to cases\.
+ **Case Fields**: Manage who can configure case fields by using the Amazon Connect console\.
  + **View Case Fields**: Allows users to view the case fields page and all of the existing case fields \(could be system or custom\)\.
  + **Edit Case Fields**: Allows users to edit any of the case fields \(for example, change title, description, single\-select options\)\.
  + **Create Case Fields**: Allows users to create new case fields\.
+ **Case Templates**: Manage who can configure case templates by using the Amazon Connect console\.
  + **View Case Fields**: Allows users to view the case fields page and all of the existing case fields \(could be system or custom\)\.
  + **Edit Case Fields**: Allows users to edit any of the case fields \(for example, change title, description, single\-select options\)\.
  + **Create Case Fields**: Allows users to create new case fields\.

When users have permissions to **View Case Fields** and **View Case Templates**, they will see the **Case fields** and **Case templates** options in their left navigation menu, as shown in the following image: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-agent-application-case-fields-menu.png)