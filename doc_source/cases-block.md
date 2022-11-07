# Flow block: Cases<a name="cases-block"></a>

**Tip**  
Be sure to [enable](enable-cases.md) Amazon Connect Cases before using this block\. Otherwise, you can't configure its properties\.

## Description<a name="create-case-description"></a>
+ Gets, updates, and creates cases\. 
+ You can link a contact to a case, and then the contact will be recorded in the **Activity feed** of the case\. When the agent accepts a contact that is linked to a case, the case automatically opens as a new tab in the agent application\.
+ While you can link contacts to multiple cases, there is a limit of five new case tabs automatically opening in the agent application\. These will be the five most recently updated cases\.
+ For more information about cases, see [Amazon Connect Cases](cases.md)\.

## Supported channels<a name="create-case-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="create-case-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties: Get case<a name="get-case-properties1"></a>

**Tip**  
The following screenshots refer to the legacy flow designer\.

When configuring properties to get a case:
+ You must provide at least one search criteria\. Otherwise this block will take the **Error** branch\.

  You can either use attribute in the Cases namespace or set manually\. If you set manually, see to the syntax in [How to persist fields throughout the flow](#cases-persist-fields)\.
+ To get cases for a given customer, add a [Customer profiles](customer-profiles-block.md) block to the flow before creating the case\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-get-case-properties5.png)

  Configure the [Customer profiles](customer-profiles-block.md) block to get the customer profile\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-get-case-properties4.png)

  In the **Cases** block, on the **Properties** page configure the **Customer ID** section as shown in the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-get-case-properties3.png)
+ You can specify to get only the last updated case for any search criteria\. This can be achieved by selecting **Get last updated case**\.
+ You can persist case fields in the case namespace to make use of them in blocks that are in your flow after the **Cases** block that is configured to **Get case**\. This can be achieved by making use of the **Response fields** section and selecting fields that you want to use in the other blocks\.

  You can either use attribute in the Cases namespace or set manually\. If you set manually, see to the syntax in [How to persist fields throughout the flow](#cases-persist-fields)\.
+ The **Get case** properties show the options for the single\-select field type\.
+ The **Get case** properties use the Contains function for text field type\.
+ The **Get case** properties use the EqualTo function for fields of type: number, boolean\.
+ The **Get case** properties use greater than or equal to for any date field search\.
+ Contacts can be routed down the following branches:
  + **Success**: The case was found\.
  + **Contact not linked**: If you specify to link the contact to case, then this error branch will appear\. It might be that the contact was not linked after the case is retrieved \(partial success/partial failure\)\. If this happens, then the flow will follow this branch\.
  + **Multiple found**: Multiple cases are found with the search criteria\.
  + **None found**: No cases are found with the search criteria\.
  + **Error**: An error was encountered while trying to find the case\. This may be due to a system error or how **Get case** is configured\.

The following images show an example of a **Get case** configuration\. The first image shows how to configure the block to search for a case by Customer ID and Title\. The Customer Id is being pulled in from the Profile ARN of the customer: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-get-case-properties1.png)

This next image shows the block configured to search by **Late Arrival**\. Three fields will be shown to the agent: **Status**, **Summary**, **Title**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-get-case-properties2.png)

## Properties: Update case<a name="update-case-properties1"></a>

When configuring properties to update a case:
+ Add a **Get case** block before an **Update case**\. Use it to find the case you want to update\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-get-case-update-case.png)
+ You must provide an update to at least one **Request** field\. Otherwise, this block takes the **Error** branch\.

  You can either use an attribute in the Cases namespace, or set the **Request** field manually\. If you set manually, see the syntax in [How to persist fields throughout the flow](#cases-persist-fields)\.
+ Contacts can be routed down the following branches:
  + **Success**: The case was updated, and the contact was linked to the case\.
  + **Contact not linked**: If you specify to link the contact to case, then this error branch will appear\. It might be that the case was updated, but the contact was not linked to the case \(partial success/partial failure\)\. If this happens, then the flow will follow this branch\.
  + **Error**: The case was not updated\. The contact was not linked to the case, as the case was not updated\.

The following images show an example of an **Update case** configuration\. The first image shows that as part of the update the contact is going to be linked to the case\. To identify which case to update, the **Case Id** is specified\. \(Case Id is the unique identifier of the case and the only field you can provide here\. Other fields will not work and produce errors\.\)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-update-case-properties1.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-update-case-properties2.png)

## Properties: Create case<a name="create-case-properties1"></a>

When configuring properties to create a case:
+ You must provide a case template\. For more information, see [Create case templates](case-templates.md)\.
+ Fields that are required appear in the **Required** fields section\. You must assign values to them to create a case\.
+ You must specify the customer to create a case\.
  + We recommend adding a [Customer profiles](customer-profiles-block.md) block to the flow before the **Cases** block\. Use the [Customer profiles](customer-profiles-block.md) block to get a customer profile with some prefetched data, or create a new customer profile and then use that to create a case\.
  + To provide a value for **Customer Id** in the **Cases** block, configure the fields as shown in the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-case-block-properties2.png)

    If you are setting the value manually, you must provide the full customer profile ARN in this format:

    `arn:aws:profile:your AWS Region:your AWS account ID:domains/profiles domain name/profiles/profile ID `
+ You can specify values for fields other than the required ones in the Request fields section\.

  You can either use attribute in the Cases namespace or set manually\. If you set manually, see to the syntax in [How to persist fields throughout the flow](#cases-persist-fields)\.
+ You can specify that a contact should be linked to case\. If you link the contact to the case, then the contact and a link to contact details appear on the case that the agent sees in the agent application\.
+ After creating a case, the case ID that is created will be persisted in the case namespace\. It can be used in other blocks by accessing the case namespace case ID attribute value\.
+ Contacts can be routed down the following branches:
  + **Success**: The case was created, and the contact was linked to the case\.
  + **Contact not linked**: If you specify to link the contact to case, then this error branch will appear\. This is because it is possible that the case was created, but the contact was not linked to the case \(partial success/partial failure\)\. If this happens, then the flow will follow this branch\.
  + **Error**: The case was not created\. The contact was not linked to the case, as the case was not created\.

The following images show an example of a **Create case** configuration\. The first image shows the new case will be created using the General inquiry template: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-create-case-properties1.png)

The next image shows the reason for the case will be set to **Shipment delayed**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-create-case-properties.png)

## How to persist fields throughout the flow<a name="cases-persist-fields"></a>

Let's say you want customers to be able to call into your contact center and get the status of their case without ever talking to an agent\. You want the IVR to read the status to the customer\. You can get the status from a system field, or you might have a custom status field, for example, named *Detailed status*\. 

Here's how to configure your flow to get and read the status to the customer: 

1. Add a **Cases** block to your flow\. Configure it to **Get case** to find the case\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-example-ivr-1.png)

1. In the **Request fields** section, search for the case by the customer **Profile ARN**:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-example-ivr-2.png )

1. In the **Response fields** section, add the field that you want passed throughout the flow\. For our example, choose **Status**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-example-ivr-3.png )

1. Add a [Play prompt](play.md) block to your flow\. 

1. Configure [Play prompt](play.md) to set the attribute manually:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-example-ivr-4.png)

   Use the following syntax for reading the status of the case to the customer:
   + For system fields, you can read the syntax and understand which field it refers to\. For example: `$.Case.status` refers to the case status\. For a list of system field IDs, see the *Field ID* column in the [System case fields](case-fields.md#system-case-fields) topic\.
   + For custom fields, the syntax uses a UUID \(unique ID\) to represent the field\. For example, in the following image, the ID for the custom field named *Detailed status* is `12345678-aaaa-bbbb-cccc-123456789012`\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-example-ivr-5.png)

## Find the custom field ID<a name="get-case-properties-find-uuid"></a>

To find the UUID of a custom field: 

1. In Amazon Connect, on the navigation menu choose **Agent applications**, **Custom fields**, and then choose the custom field that you want\.

1. While on the details page for the custom field, look at the URL of the page\. The UUID is the last portion of the URL\. For example, in the following URL:

   `https://instance alias.my.connect.aws/cases/configuration/fields/update/12345678-aaaa-bbbb-cccc-123456789012`

   The UUID is `12345678-aaaa-bbbb-cccc-123456789012`\.

The following image shows where you find the custom field ID in the URL:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-block-custom-field-uuid.png)

## Configuration tips<a name="create-case-tips"></a>
+ Be sure to check the [Cases service quotas](amazon-connect-service-limits.md#cases-quotas), and request increases\. The quotas apply when this block creates cases\.

## Configured block<a name="create-case-configured"></a>

When this block is configured to create a cases, it looks similar to the following: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-case-block-configured.png)