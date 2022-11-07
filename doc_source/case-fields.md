# Create case fields<a name="case-fields"></a>

*Case fields* are the building blocks for *case templates*\. You create all of the possible fields of information \(for example, VIN number, policy number, make/model of car\) that you want agents to collect for a given customer issue\. 

 After you create case fields, you can create case templates\.

There are two types of case fields:
+ [System case fields](#system-case-fields): Amazon Connect provides system fields\. You cannot change the name or description\.
+ [Custom case fields](#custom-case-fields): You can create custom case fields that are specific for your business\. You must name the case field, and optionally provide a description\. Note that the description appears only in the Amazon Connect console\. It doesn't appear to agents\.

## How to create case fields<a name="how-to-create-case-fields"></a>

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create fields\. For a list of required permissions, see [Security profile permissions for Cases](assign-security-profile-cases.md)\.

1. Verify the quota for case fields and request an increase if needed\. For more information, see [Amazon Connect Cases service quotas](amazon-connect-service-limits.md#cases-quotas)\.

1. On the left navigation menu, choose **Agent applications**, **Case fields**\.

1. The first time you create new fields, you'll notice several [system fields](#system-case-fields) are already present\. You cannot change the name of these fields, but in some cases you can edit them\. 

   For example, **Case Id** is a system field\. When a case is created, Amazon Connect adds a case ID automatically, and you cannot change it\. **Case reason** is also a system field but you can edit it and enter reasons that are specific to your contact center\.

1. Choose **\+ New field**\.

1. Select the type of field you want to create\. For example, you might choose **Text** if you want agents to be able to enter free form notes\.

1. Assign a name to the field\. It will appear to agents in the agent application\.

1. Optionally, provide a description\. It will only appear to admins on the Amazon Connect console\. It does not appear to agents in the agent application\.

1. Choose **Save**\.

1. When you're done adding fields, you're ready to [create a template](case-templates.md)\.

## System case fields<a name="system-case-fields"></a>

Amazon Connect provides system fields\. You cannot change the name or description of a system field\.

The following table lists the system case fields:


| Field name | Field ID \(how you call the field in the API\) | Field type | Description | Where the data comes from | 
| --- | --- | --- | --- | --- | 
|  Case ID  |  case\_id  | text | Unique Identifier of the case in UUID format \(for example, 689b0bea\-aa29\-4340\-896d\-4ca3ce9b6226\) | Amazon Connect | 
|  Case Reason  |  case\_reason  | single\-select | The reason for opening the case | Agent | 
|  Customer  |  customer\_id  | text | The full ARN of the customer profile identified for the case is required when using the API\. On the Cases: Fields page, the customer's name is displayed\. | Amazon Connect | 
|  Date/Time Closed  |  last\_closed\_datetime  | date\-time | The date and time the case was last closed\. It does not guarantee that a case is closed\. If a case is reopened, this field contains the date/time stamp of the last time the status was changed to closed\. | Amazon Connect | 
|  Date/Time Opened  |  created\_datetime  | date\-time | The date and time the case was opened\. | Amazon Connect | 
|  Date/Time Updated  |  last\_updated\_datetime  | date\-time | The date and time the case was last updated\. | Amazon Connect | 
|  Reference number  |  reference\_number  | text | A friendly number for the case in 8\-digit numeric format\. Reference numbers \(unlike the Case ID\) are not guaranteed to be unique\. We recommend that you identify the customer and then collect the reference number to correctly find the right case\.  | Agent | 
|  Status  |  status  | single\-select | Current status of the case  | Agent | 
|  Summary  |  summary  | text | Summary of the case  | Agent | 
|  Title  |  title  | text | Title of the case  | Agent | 

## Custom case fields<a name="custom-case-fields"></a>

You can create custom case fields that are specific for your business\. You must name the case field, and optionally provide a description\. Note that the description appears only in the Amazon Connect console\. It doesn't appear to agents\.

You can create fields that are type: number, text, single\-select, or true/false\.

### Single\-select fields<a name="single-select-case-fields"></a>

For single\-select case fields, whether system or custom, you can add value options that the field can take\. For example, you can add options to the single\-select system field Case reason such as **General inquiry**, **Billing issue**, or **Product defect**, that reflect the types of issues in your contact center\. 

#### About the Status field<a name="status-single-select-field"></a>

You can add options to the single\-select **Status** field, such as **Investigating** or **Escalated to manager**\. The field comes with two options, **Open** and **Closed**, which cannot be changed\.

#### Active/inactive field options<a name="active-inactive-single-select-field"></a>

Single\-select case fields can be active or inactive\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-single-select-active-inactive.png)
+ **Active**: If a field option is active, it means that the field can be given that option\. For example, based on the following image, the Status field can be set to **Closed**, **Open**, or **Pending**, as these are the only active options\.
+ **Inactive**: If you make the **Pending** option inactive, then the field can no longer be given that option\. Any existing cases remain unchanged and can still have the status as **Pending**\.

Single\-select options have two parts:

1. Option name \(shown to agents\): The label that is displayed to agents in the agent application\.

1. Option value \(internal reference\): The data that's collected\. For example, for AWS Region, you may want to display **US West \(Oregon\)** but collect the data as **PDX**\. 

   Field options appear to the agent in alphabetical order\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-single-select-names.png)