# Tag\-based access control<a name="tag-based-access-control"></a>

Tag\-based access controls enable you to configure granular access to specific resources based on assigned resource tags\. You can configure tag based access controls by using the API/SDK or within the Amazon Connect console \(for supported resources\)\.

## Tag\-based access control using the API/SDK<a name="tag-based-access-control-api-sdk"></a>

To use tags to control access to resources within your AWS accounts, you need to provide tag information in the condition element of an IAM policy\. For example, to control access to your Voice ID domain based on the tags you've assigned to it, use the `aws:ResourceTag/key-name` condition key, along with a specific operator like `StringEquals` to specify which tag *key:value* pair must be attached to the domain, in order to allow given actions for it\.

For more detailed information on tag\-based access control, see [Controlling access to AWS resources using tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html) in the IAM User Guide\.

## Tag\-based access control using the Amazon Connect console<a name="tag-based-access-control-connect-ui"></a>

A *resource* tag is a custom metadata label that you can add to a resource in order to make it easier to identify, organize, and find in a search\. You can apply tags programmatically using the Amazon Connect SDK/APIs, and for certain resources you can apply tags from within the Amazon Connect console\. To learn more about resource tags, see [Tagging resources in Amazon Connect](tagging.md)\.

An access control tag is similar to a resource tag in that it uses the same *Key:value* structure\. However, the distinction with an access control tag is that it introduces authorization controls that limit a user’s access, to only specified resources containing resource tags with identical *Key:value* pairs\. Access control tags are defined within security profiles, by first selecting the resource \(routing profile, queue, users, etc\.\) for which to control access to, and then defining the *Key:value* pair to match on\. Once a security profile with access control tags has been applied to a user, it will limit the user's access based on the defined combination of the selected resource\(s\) and access control tag\(s\) \(*Key:value*\)\. Without access control tags applied, a user will be able to see all resources if given permission to do so\.

To use tags to control access to resources within the admin website of your Amazon Connect instance, you need to configure the access control section within a given security profile\. For example, to control access to a routing profile based on the tags you've assigned to it, you would specify the routing profile as an access controlled resource, and then specify which tag *Key:value* pair you would like to enable access to\.

## Configuration limitations<a name="tag-based-access-control-config-limitations"></a>

Access control tags are configured on a security profile\. You can configure up to two access control tags on a single security profile\. Adding additional access control tags will make that security profile more restrictive\. For example if you were to add two access control tags like `Department:X` and `Country:Y`, the user would only be able to see resources containing both tags\.

Users can be assigned a maximum of one security profile that contains access control tags\. They can have other security profiles, as long as those additional security profiles do not contain tags\. In the scenario where multiple security profiles are present with overlapping resource permissions, the security profile without tag based access controls will be enforced over the one with tag based access controls\.

Service linked roles are required in order to configure [resource tags](https://docs.aws.amazon.com/connect/latest/adminguide/tagging.html) or [access control tags](https://docs.aws.amazon.com/connect/latest/adminguide/tag-based-access-control.html)\. If your instance was created after October 2018, this will be available by default with your Amazon Connect instance\. However if you have an older instance, please refer to [Use service\-linked roles for Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/connect-slr.html) for instructions for how to enable service linked roles\.

## Amazon Connect tagging best practices<a name="tag-based-access-control-best-practices"></a>

Applying tag based access controls is an advanced configuration feature that is supported by Amazon Connect and that follows the AWS shared responsibility model\. It is important to ensure that you are correctly configuring your instance to comply with your desired authorization needs\. For more information, please review the [AWS shared responsibilities model](http://aws.amazon.com/compliance/shared-responsibility-model/)\.

Ensure that you have enabled at least *view* permissions for the resources that you enable tag based access control for\. This will ensure that you avoid permission inconsistencies that result in denied access requests\.

Tag based access controls are enabled at the resource level, which means that each resource can be restricted independently\. In certain use cases this may be acceptable but it is considered best practice to enable tag based access controls to all resources together\. For example, enabling access to users but not security profiles, would allow a user to create a security profile with privileges that supersede your intended user access control settings\.

When logged in to the Amazon Connect console with tag based access controls applied, users will not be able to access historical change logs for the resources that they are restricted on\.

As a best practice, you should disable access to the following resources/modules when applying tag based access controls within the Amazon Connect console\. If you do not disable access to these resources, users with tag based access controls on a particular resource that view these pages may see an unrestricted list of users, security profiles, routing profiles, or queues\. For more information on how to manage permissions, see [List of security profile permissions](security-profile-list.md)\.


| Modules | Permission to disable access | 
| --- | --- | 
| Agent activity audit | Agent activity audit | 
| Contact search | Contact Search | 
| Dashboard | Access metrics | 
| Flow/Flow module | Contact flow modules \- View | 
| Forecasting | Forecasting | 
| Historical changes/Audit portal | Access metrics | 
| Historical metrics | Historical metrics | 
| Login/Login out report | Login/Logout report \- View | 
| Outbound Campaign | Campaigns \- View | 
| Quick connect | Quick connects \- View | 
| Rules | Rules \- View | 
| Saved reports | Saved reports \- View | 
| Scheduling | Schedule manager | 