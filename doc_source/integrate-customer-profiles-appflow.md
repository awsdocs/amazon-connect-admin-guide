# Set up integration for Salesforce, ServiceNow, Marketo, or Zendesk<a name="integrate-customer-profiles-appflow"></a>

These integrations use Amazon AppFlow to provide periodic updates to Amazon Connect Customer Profiles\.

## Before you begin<a name="before-you-begin-cp-integration"></a>

### Bulk ingestion of data<a name="bulk-ingestion"></a>

When you set up your integration, you are prompted to enter a date how far back you want to go to ingest data\. If you choose a date that is more than two months ago, Customer Profiles automatically enables bulk ingestion by creating multiple flows\. It does this so you don't have to calculate how many flows you need to ingest data\. 

When automatic bulk ingestion is enabled, Customer Profiles does the following:
+ Sets the batch size to two months\.
+ Retries on transient failures up to three times before failing\.

You can use the [CreateIntegrationWorkflowRequest](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/CreateIntegrationWorkflowRequest .html) API to call your own batch size\.

### Why am I asked to select or create an IAM role?<a name="why-create-iam-role"></a>

For Salesforce, Marketo, and ServiceNow, Customer Profiles helps improve the historical ingestion of these sources by using your IAM role to create several workflows to ingest your data quickly and efficiently\. 

 For these sources, if you select more than 60 days back in the **Date for importing records** date picker, you will be prompted to create a new IAM role or select an existing one\. This role allows Customer Profiles to manage your integration\. It provides Customer Profiles with the necessary permissions to update and create a workflow to ingest your data\. After the workflow is complete, Customer Profiles creates a standard, continuous integration that ingests your new data as it is updated in your source\. 

The role created in the console is only useable by the domain it was created on\. This is because Amazon Connect limits the access of the role to only the KMS key used by the domain\. 

For more information, see [Grant least privilege access to your Customer Profiles execution role](#grant-least-privilege-cp)\.

## Integration setup steps<a name="steps-integrate-cp-salesforce-servicenow"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the **Instances** page, choose the instance alias\. The instance alias is also your instance name, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Customer profiles**\.

1. On the **Customer profiles configuration** page, choose **Add integration**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-addintegration.png)

1. On the **Select source** page, choose which external application you want to get customer profiles data from: Salesforce, Zendesk, ServiceNow, or Marketo\. Select **I’ve read the integration requirements** to indicate you understand the connection requirements for your application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-choose-app.png)

1. On the **Establish connection** page, choose one of the following: 
   + **Use existing connection**: This allows you to reuse existing Amazon AppFlow resources you may have created in your AWS account\.\.
   + **Create new connection**: Enter the information required by the external application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-establish-connection.png)

1. On the **Integration options** page, choose which source objects you want to ingest and select their object type\. 

   Object types store your ingested data\. They also define how objects from your integrations are mapped to profiles when they are ingested\. Customer Profiles provides default object type templates you can use that define how attributes in your source objects are mapped to the standard objects in Customer Profiles\. You can also use the object mappings that you’ve created from the [PutProfileObjectType](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutProfileObjectType.html)\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-integration-options.png)

1. For the **Ingestion start date**, Customer Profiles starts ingesting records created after this date\. By default, the date for importing records is set at 30 days prior\.

1. On the **Review and integrate** page, check that the **Connection status** says **Connected**, and then choose **Create integration**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-review-and-integrate.png)

1. After the integration is set up, back on the **Customer profiles configuration** page, choose **View objects** to see what data is being batched and sent\. Currently, this process ingests records that were created or modified in the last 30 days\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-objects.png)

## Grant least privilege access to your Customer Profiles execution role<a name="grant-least-privilege-cp"></a>

If you want to create your own IAM role, we recommend using the permissions shown in the following code to limit the role to the least permissions needed\. Use the snippet below to create your role manually\. Use your own KMS key and specify your Region where needed\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Condition": {
                "ForAnyValue:StringEquals": {
                    "aws:RequestTag/awsOwningService": "customer-profiles-integration-workflow"
                }
            },
            "Action": [
                "appflow:CreateFlow",
                "appflow:TagResource",
                "profile:TagResource",
                "profile:PutIntegration"
            ],
            "Resource": "*",
            "Effect": "Allow",
            "Sid": "CreateFlowResources"
        },
        {
            "Action": [
                "appflow:UseConnectorProfile"
            ],
            "Resource": "*",
            "Effect": "Allow",
            "Sid": "UseConnectorResources"
        },
        {
            "Condition": {
                "ForAnyValue:StringEquals": {
                    "aws:ResourceTag/awsOwningService": "customer-profiles-integration-workflow"
                }
            },
            "Action": [
                "appflow:DescribeFlow",
                "appflow:DescribeFlowExecutionRecords",
                "appflow:DeleteFlow",
                "appflow:StartFlow",
                "appflow:StopFlow",
                "appflow:UpdateFlow",
                "profile:DeleteIntegration"
            ],
            "Resource": "*",
            "Effect": "Allow",
            "Sid": "AccessFlowResources"
        },
    {
      "Action": [
        "kms:CreateGrant",
        "kms:ListGrants"
      ],
      "Resource": "{{YourKMSKeyConsumedByTheDomain}}",
      "Condition": {
        "StringEquals": {
          "kms:ViaService": [
            "appflow.{{region}}.amazonaws.com"
          ]
        }
      },
      "Effect": "Allow",
      "Sid": "KMSAppflow"
    },
    {
      "Action": [
        "kms:CreateGrant"
      ],
      "Resource": "{{YourKMSKeyConsumedByTheDomain}}",
      "Condition": {
        "StringEquals": {
          "kms:ViaService": [
            "profile.{{region}}.amazonaws.com"
          ]
        },
        "ForAllValues:StringEquals": {
          "kms:GrantOperations": [
            "Decrypt"
          ]
        }
      },
      "Effect": "Allow",
      "Sid": "KMSCustomerProfiles"
    }
  ]
}
```

## Monitor your Customer Profiles integrations<a name="monitor-customer-profile-connection"></a>

After your connection is established, if it stops working, delete the integration and then re\-establish it\. 

## What to do if objects aren't being sent<a name="fix-customer-profile-connection"></a>

If an object fails to be sent, choose **Flow details** to learn more about what's gone wrong\. 

You may need to delete the configuration and re\-connect to the external application\. 