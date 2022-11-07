# Using service\-linked roles for Amazon AppIntegrations<a name="appintegrations-slr"></a>

Amazon AppIntegrations uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to Amazon AppIntegrations\. Service\-linked roles are predefined by Amazon AppIntegrations and include all the permissions that the service requires to call other AWS services on your behalf\.

A service\-linked role makes setting up Amazon AppIntegrations easier because you don’t have to manually add the necessary permissions\. Amazon AppIntegrations defines the permissions of its service\-linked roles, and unless defined otherwise, only Amazon AppIntegrations can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting their related resources\. This protects your Amazon AppIntegrations resources because you can't inadvertently remove permission to access the resources\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-linked roles** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for Amazon AppIntegrations<a name="slr-permissions-appinteg"></a>

Amazon AppIntegrations uses the service\-linked role named **AWSServiceRoleForAppIntegrations** which allows AppIntegrations to access AWS services and resources on your behalf\.

The AWSServiceRoleForAppIntegrations service\-linked role trusts the following service to assume the role:
+ `app-integrations.amazonaws.com`

The role permissions policy named AppIntegrationsServiceLinkedRolePolicy allows Amazon AppIntegrations to complete the following actions on the specified resources:

```
     {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "cloudwatch:PutMetricData"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "cloudwatch:namespace": "AWS/AppIntegrations"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "appflow:DescribeConnectorEntity",
                "appflow:ListConnectorEntities"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "appflow:DescribeConnectorProfiles",
                "appflow:UseConnectorProfile"
            ],
            "Resource": "arn:aws:appflow:*:*:connector-profile/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "appflow:DeleteFlow",
                "appflow:DescribeFlow",
                "appflow:DescribeFlowExecutionRecords",
                "appflow:StartFlow",
                "appflow:StopFlow",
                "appflow:UpdateFlow"
            ],
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/AppIntegrationsManaged": "true"
                }
            },
            "Resource": "arn:aws:appflow:*:*:flow/FlowCreatedByAppIntegrations-*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "appflow:TagResource"
            ],
            "Condition": {
                "ForAllValues:StringEquals": {
                    "aws:TagKeys": [
                        "AppIntegrationsManaged"
                    ]
                }
            },
            "Resource": "arn:aws:appflow:*:*:flow/FlowCreatedByAppIntegrations-*"
        }
    ]
}
```
+ Action: `cloudwatch:PutMetricData` on `"*"` using the `StringEquals` condition `"cloudwatch:namespace": "AWS/AppIntegrations"`\.
+ Action: `appflow:DescribeConnectorEntity` and `appflow:ListConnectorEntities` on `"*"`\.
+ Action: `appflow:DescribeConnectorProfiles` and `appflow:UseConnectorProfile` on ` arn:aws:appflow:*:*:connector-profile/*` 
+ Action: `appflow:DeleteFlow`, `appflow:DescribeFlow`, `appflow:DescribeFlowExecutionRecords`, `appflow:StartFlow`, `appflow:StopFlow`, and `appflow:UpdateFlow` on ` arn:aws:appflow:*:*:flow/FlowCreatedByAppIntegrations-*` using the `StringEquals` condition `"aws:ResourceTag/AppIntegrationsManaged": "true"`\. 
+ Action: `appflow:TagResource` on `arn:aws:appflow:*:*:flow/FlowCreatedByAppIntegrations-*` using the `ForAllValues:StringEquals aws:TagKeys` condition `AppIntegrationsManaged`\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-linked role permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a service\-linked role for Amazon AppIntegrations<a name="create-slr-appinteg"></a>

You don't need to manually create a service\-linked role\. When you create a data or event integration using either the Wisdom, Customer Profiles, or Tasks widget in Amazon Connect in the AWS Management Console, the AWS CLI, or the AWS API, Amazon AppIntegrations creates the service\-linked role for you\. 

**Important**  
This service\-linked role can appear in your account if you completed an action in another service that uses the features supported by this role\. Also, if you created any new Amazon AppIntegrations resources after September 30, 2022, when it began supporting service\-linked roles, then Amazon AppIntegrations created the AWSServiceRoleForAppIntegrations role in your account\. To learn more, see [A new role appeared in my IAM account](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html#troubleshoot_roles_new-role-appeared)\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create a data or event integration using either the Wisdom, Customer Profiles, or Tasks widget in Amazon Connect, Amazon AppIntegrations creates the service\-linked role for you again\. 

You can also use the IAM console to create a service\-linked role with the **AppIntegrations** use case\. In the AWS CLI or the AWS API, create a service\-linked role with the `app-integrations.amazonaws.com` service name\. For more information, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\. If you delete this service\-linked role, you can use this same process to create the role again\.

## Editing a service\-linked role for Amazon AppIntegrations<a name="edit-slr-appinteg"></a>

Amazon AppIntegrations does not allow you to edit the AWSServiceRoleForAppIntegrations service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a service\-linked role for Amazon AppIntegrations<a name="delete-slr-appinteg"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\. You must first delete your data and event integration associations in the AWS Console and then delete your data and event integrations using the AWS CLI\.

**Note**  
If the Amazon AppIntegrations service is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete data integration associations used by the AWSServiceRoleForAppIntegrations in the AWS Console**

1. Go to the Wisdom section of the Amazon Connect Console and choose the name of the data integration association that you wish to delete\.

1. Choose **Delete** on the right hand side of the **Integration details** section\.

1. In the pop\-box, enter the name of the integration for confirmation and choose **Delete**\.

**To delete data integrations used by the AWSServiceRoleForAppIntegrations using the AWS CLI**

1. List your data integrations in order to view the names of your existing integrations\.

   `aws appintegrations list-data-integrations`

1. Delete each integration using the data integration name\.

   `aws appintegrations delete-data-integration --data-integration-identifier DATA_INTEGRATION_NAME`

**To delete event integration associations used by the AWSServiceRoleForAppIntegrations in the AWS Console**

1. Go to the Customer Profiles or the Tasks section of the Amazon Connect Console and choose the name of the event integration association that you wish to delete\.

1. Once you choose an event integration on the Tasks section, a pop\-up will appear\. Choose the **Remove connection** button and enter the word *remove* to delete your event integration association\.

**To delete event integrations used by the AWSServiceRoleForAppIntegrations using the AWS CLI**

1. List your event integrations in order to view the names of your existing integrations\.

   `aws appintegrations list-event-integrations`

1. Delete each integration using the data integration name\.

   `aws appintegrations delete-event-integration --name EVENT_INTEGRATION_NAME`

**To manually delete the service\-linked role using IAM**

Use the IAM console, the AWS CLI, or the AWS API to delete the AWSServiceRoleForAppIntegrations service\-linked role\. For more information, see [Deleting a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported regions for Amazon AppIntegrations service\-linked roles<a name="slr-regions-appinteg"></a>

Amazon AppIntegrations supports using service\-linked roles in all of the regions where the service is available\. For more information, see [AWS regions and endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html)\.

You can use the AWSServiceRoleForAppIntegrations role in the following regions\.


****  

| Region name | Region identity | Support in Amazon AppIntegrations | 
| --- | --- | --- | 
| US East \(N\. Virginia\) | us\-east\-1 | Yes | 
| US West \(Oregon\) | us\-west\-2 | Yes | 
| Asia Pacific \(Mumbai\) | ap\-south\-1 | Yes | 
| Asia Pacific \(Seoul\) | ap\-northeast\-2 | Yes | 
| Asia Pacific \(Singapore\) | ap\-southeast\-1 | Yes | 
| Asia Pacific \(Sydney\) | ap\-southeast\-2 | Yes | 
| Asia Pacific \(Tokyo\) | ap\-northeast\-1 | Yes | 
| Canada \(Central\) | ca\-central\-1 | Yes | 
| Europe \(Frankfurt\) | eu\-central\-1 | Yes | 
| Europe \(London\) | eu\-west\-2 | Yes | 
| Africa \(Cape Town\) | af\-south\-1 | Yes | 