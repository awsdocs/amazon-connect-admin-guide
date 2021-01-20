# Make Customer Profiles available to your agents<a name="customer-profile-access"></a>

After you enable Amazon Connect Customer Profiles, you need to make the feature available to your agents\. Do the following:
+ Use the Amazon Connect Streams library to embed the Customer Profiles app into your own agent experience, such as an agent web site\. This site is the same location that has CCP\. For more information, see [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams)\.

  Using CCP out\-of\-the\-box with Customer Profiles is in preview\. To be added to the preview, provide your Amazon Connect instance ID on this [AWS \- Contact Us](https://pages.awscloud.com/profiles-agent-app-preview.html) page\.
+ Assign the following **Customer profile** permissions as needed to the agent's security profile:
  + **View**: Enables the user to see the Customer profiles application\. They can to search for profiles, view details stored in customer profiles \(for example, Name, Address\), and associate Contact Records to profiles\.
  + **Edit**: Enables the user to edit details in the customer profile \(for example, change address\)\. They inherit **View** and **Create** permissions by default\.
  + **Create**: Enables users to create and save a new profile\. They inherit **View** permissions by default, but don't inherit **Edit** permissions\.

  For instructions, see [Update security profiles](update-security-profiles.md)\.

  By default, the following security profiles already have permissions to perform all Customer profiles activities: **Admin**, **Agent**, **Call Center Manager**\.