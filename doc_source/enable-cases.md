# Enable Cases<a name="enable-cases"></a>

This topic explains how to enable Amazon Connect Cases using the Amazon Connect console\. To use the API, see [Amazon Connect Cases API Reference](https://docs.aws.amazon.com/cases/latest/APIReference/Welcome.html)\.

**Tip**  
A case is always associated with a customer profile\. You must have Customer Profiles enabled\. Check your instance settings in the Amazon Connect console, and if a Customer Profiles domain does not yet exist, see [Enable Customer Profiles for your instance](enable-customer-profiles.md)\.

## Requirements<a name="cases-iam-requirements"></a>

If you're using custom IAM policies to manage access to the Amazon Connect Cases, your users need the following IAM permissions to onboard to Cases using the Amazon Connect console:
+ `connect:ListInstances`
+ `ds:DescribeDirectories`
+ `connect:ListIntegrationAssociations`
+ `cases:GetDomain`
+ `cases:CreateDomain`
+ `connect:CreateIntegrationAssociation`
+ `connect:DescribeInstance`
+ `iam:PutRolePolicy`

For more information, see [Required permissions for using custom IAM policies to manage Cases](required-permissions-iam-cases.md)\.

## How to enable Amazon Connect Cases<a name="how-to-enable-cases"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. On the left navigation menu, choose **Cases**\. This option is currently available in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.

1. Choose **Enable cases** to get started\.

1. On the **Cases** page, choose **Add domain**\. 

1. On the **Add domain** page, enter a unique, friendly name that's meaningful to you, such as your organization name\.

1. Choose **Add domain**\. The domain is created\.

   If the domain is not created, choose **Try again**\. If that doesn't work, contact AWS Support\.

## Next steps<a name="enable-cases-next-steps"></a>

After your cases domain is created, do the following:

1. [Assign security profile permissions](assign-security-profile-cases.md) to agents and call center managers\.

1. [Create case fields](case-fields.md)\. Fields are the building blocks of your case templates\.

1. [Create case templates](case-templates.md)\. Case templates are forms that agents complete and reference in the agent application\. Templates ensure the right information is collected and referenced for different types of customer issues\.

1. Optionally, add the [Cases](cases-block.md) block to your flows\. This block enables you to get, update, or create cases automatically\.

1. Optionally, set up [case event streams](case-event-streams.md) to get near real\-time updates when cases are created or modified\.