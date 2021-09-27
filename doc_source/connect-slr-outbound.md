# Use service\-linked roles for Amazon Connect High\-Volume Outbound Communications<a name="connect-slr-outbound"></a>

Amazon Connect High\-Volume Outbound Communications uses AWS Identity and Access Management service\-linked roles\. When an Amazon Connect instance is enabled to use High\-Volume Outbound Communications, a unique service linked role is created by Amazon Connect High\-Volume Outbound Communications which allows it to perform actions on the Amazon Connect Instance\.

A service\-linked role makes setting up Amazon Connect High\-Volume Outbound Communications easier because you don't have to manually add the necessary permissions\. Amazon Connect High\-Volume Outbound Communications defines the permissions of its service\-linked roles, and unless defined otherwise, only Amazon Connect High\-Volume Outbound Communications can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\. 

For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\. Look for the services that have **Yes** in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\. 

## Service\-linked role permissions for Amazon Connect High\-Volume Outbound Communications<a name="slr-permissions-outbound"></a>

Amazon Connect High\-Volume Outbound Communications uses the service\-linked role prefixed `AWSServiceRoleForConnectCampaigns`—Grants Amazon Connect High\-Volume Outbound Communications permission to access AWS resources on your behalf\.

The `AWSServiceRoleForConnectCampaigns` service\-linked role trusts the following services to assume the role: 
+ `connect-campaigns.amazonaws.com`

The role permissions policy allows Amazon Connect High\-Volume Outbound Communications to complete the following actions on the specified resources: 
+ Action: Amazon Connect High\-Volume Outbound Communications `connect-campaigns:ListCampaigns` for the AWS account\.
+ Action: Amazon Connect `connect:StartOutboundVoiceContact` `connect:GetMetricData` and `connect:GetCurrentMetricData` for the Amazon Connect instance specified\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-linked role permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\. 

## Create a service\-linked role for Amazon Connect High\-Volume Outbound Communications<a name="create-slr-outbound"></a>

You don't need to manually create a service\-linked role\. When you associate an Amazon Connect instance with Amazon Connect High\-Volume Outbound Communications by invoking `PutConnectInstanceConfig` API, Amazon Connect High\-Volume Outbound Communications creates the service\-linked role for you\. 

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you associate a new Amazon Connect instance with Amazon Connect High\-Volume Outbound Communications, Amazon Connect High\-Volume Outbound Communications creates the service\-linked role for you again\. 

## Edit a service\-linked role for Amazon Connect High\-Volume Outbound Communications<a name="edit-slr-outbound"></a>

Amazon Connect High\-Volume Outbound Communications does not allow you to edit the `AWSServiceRoleForConnectCampaigns` service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\. 

## Delete a service\-linked role for Amazon Connect High\-Volume Outbound Communications<a name="delete-slr-outbound"></a>

If you no longer need Amazon Connect High\-Volume Outbound Communications, we recommend that you delete the associated service\-linked role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

To delete Amazon Connect High\-Volume Outbound Communications resources used by the `AWSServiceRoleForConnectCampaigns`
+ Delete all campaigns setup for the AWS account\.
+ For this public preview, contact AWS support to delete all configuration so the service\-linked role can be deleted safely\.

**To manually delete the service\-linked role using IAM**
+ Use the IAM console, the AWS CLI, or the AWS API to delete the `AWSServiceRoleForConnectCampaigns` service\-linked role\. For more information, see [Deleting a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for Amazon Connect High\-Volume Outbound Communications service\-linked roles<a name="regions-slr-outbound"></a>

Amazon Connect High\-Volume Outbound Communications supports using service\-linked roles in all of the Regions where the service is available\. For more information, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#connect_region)\. 