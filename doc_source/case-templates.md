# Create case templates<a name="case-templates"></a>

*Case templates* are forms that ensure agents collect and reference the right information for different types of customer issues\. For example, you can create a case template for vehicle damage issues, and require agents complete certain fields when they talk to a customer filing an insurance claim\. 

When you create a case template, you choose the name that appears to agents, the fields on the form, and the order of the fields\.

**Important**  
Cases are always created based on a template\.

## How case templates look in the agent application<a name="agent-case-template"></a>

In the agent application, the agent sees the case fields in a Z\-formation: case fields are displayed in two columns from left to right, top to bottom\.

![\[A case in the agent workspace.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-agent-side.png)

When you're building a case template, think of the information in the agent application as being is divided into two sections where case fields are displayed to the agent: 

![\[A case template.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-templates-agent-application.png)
+ Top fields: This section is always visible on the case, even when agent is viewing sub\-sections of the case \(for example, **Activity Feed** or **Comments**\)\.
+ More information: This is a tabbed subsection of the case\. It is visible when agent is viewing another subsection, such as **Activity Feed** or **Comments**\.

When you create and edit a template, you can do the following in each section:
+ Change the order of the fields\.
+ Indicate if fields are required\.

Some system fields, such as **Title** and **Status**, appear on all cases and are required\. Other system fields, such as **Customer**, **Summary**, and **Reference number**, appear by default on the case details page\. You can remove or rearrange these fields\.

Each case that is created is connected to a customer profile from your Amazon Connect instance\. On new case templates, the customer name appears by default on the case details page\. You can remove or rearrange this field from your templates from the Amazon Connect console\.

## How to create a template<a name="how-to-create-template"></a>

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create templates\. For a list of required permissions, see [Security profile permissions for Cases](assign-security-profile-cases.md)\.

1. Verify the quota for case templates and request an increase if needed\. For more information, see [Amazon Connect Cases service quotas](amazon-connect-service-limits.md#cases-quotas)\.

1. Verify the [case fields](case-fields.md) you want to add to your case template have already been created\.

1. On the left navigation menu, choose **Agent applications**, **Case templates**\.

1. Choose **\+ New Template**\.

1. Assign a name to the template\. It will appear to agents in the agent application\. The following image shows an example of how templates appear, by default in alphabetical order:  
![\[A case template.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/case-templates-in-agent-application.png)

1. In the **Top fields** section, you'll see some system fields already there\. Choose **Add fields**, and use the dropdown to choose the field\. Fields that are gray\-out are already a part of the template\. If you want agents to complete the field in order to save the form, choose **Required**\.

1. In the **More information** section, choose the fields you want to appear\.

1. When you're done, choose **Save**\. The template is immediately made available to agents in the agent application\.