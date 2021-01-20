# Assign permissions to review recordings of past conversations<a name="assign-permssions-to-review-recordings"></a>

**To assign a manager permissions to review recordings of past conversations**

1. Go to **Users**, **User management**, choose the manager, and then choose **Edit**\.

1. In the Security Profiles box, assign the manager to the **CallCenterManager** security profile\. This security profile also includes a setting that makes **the icon to download recordings appear in the results of the **Contact search page\. 

1. If you also want the manager to monitor live conversations, assign the manager to the **Agent** security profile so they can access the Contact Control Panel \(CCP\)\. This is so they can monitor the conversation through the CCP\.

1. For the manager to listen to recordings that have been redacted, assign **Recorded conversations \(redacted\)** permissions to the security profile\. For more information about these permissions, see [Security profile permissions for Contact Lens](permissions-for-contact-lens.md)\.

   The redaction feature is provided as part of Contact Lens for Amazon Connect\. For more information, see [Use sensitive data redaction](sensitive-data-redaction.md)\.

1. Choose **Save**\. 

**Or, to create a new security profile specific for this purpose**

1. Choose **Users**, **User management**, **Security profiles**\. 

1. Choose **Add new security profile**\. 

1. Expand **Metrics and Quality**, then choose **Manager monitor** and **Recorded conversations** \(choose both **Access** and **Enable download button**\)\. 

1. If you also want the manager to monitor live conversations, assign the manager to the **Agent** security profile so they can access the Contact Control Panel \(CCP\)\. This is so they can monitor the conversation through the CCP\.

1. For the manager to listen to recordings that have been redacted, assign **Recorded conversations \(redacted\)** permissions to the security profile\. For more information about these permissions, see [Security profile permissions for Contact Lens](permissions-for-contact-lens.md)\.

1. Choose **Save**\. 