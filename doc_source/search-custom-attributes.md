# Search by custom contact attributes<a name="search-custom-attributes"></a>

You can create search filters based on custom contact attributes \(also called [user\-defined contact attributes](connect-attrib-list.md#user-defined-attributes)\)\. For example, if you add `AgentLocation` and `InsurancePlanType` to your contact records as custom attributes, you can search for contacts with specific values in these attributes, such as calls handled by agents located in Seattle, or calls made by customers who purchased homeowners insurance\.

## Required permissions to configure searchable contact attributes<a name="permissions-search-custom-attributes"></a>

By default, a custom attribute isn't indexed until someone with appropriate permissions, such as an admin or manager, specifies it should be searchable\. You grant permissions to select users so they can configure which custom contact attributes can be added as a search filter\. 

Assign the following permissions to their security profile:
+ **Contact search**: Controls basic access to the **Contact search** page\. 
+ **Contact attributes**: Allows users to view contact attributes\. Also controls access to the search filters based on contact attributes\.
+ **Configure searchable contact attributes** \- **All**: People who have this permission determine what custom data will be searchable \(by people who have the **Contact attributes** permission\)\. It allows them to access the following configuration page:   
![\[The search customer contact attributes page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-custom-attributes-configuration-page.png)

## Configure searchable custom contact attributes<a name="configure-search-custom-attributes"></a>

1. On the **Contact search** page, choose **Add filter**, **Custom contact attribute**\. Only people with **Configure searchable contact attributes** permissions in their security profile see this option\.  
![\[The contact search page, the filters dropdown menu, the Customer contact attribute option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-custom-attributes-specify1.png)

1. The first time you choose **Custom contact attribute**, the following box appears, indicating no attributes have been configured for this Amazon Connect instance\. Choose **Specify searchable attribute keys**\.  
![\[The add filter option, a message that no keys have been specified for search.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-custom-attributes-specify2.png)

1. In the **Attribute key** box, type the name of your custom attribute, and then choose **Add key**\.
**Important**  
You must type the exact key name\. It is case sensitive\.

1. When finished, choose **Save**\.

Your users will be able to search on these keys for any future contacts\.

## Edit, add, or remove contact attributes<a name="edit-add-remove-attribute-keys"></a>

To edit, add, or remove keys, choose **Attribute**, **Settings**\. If you don't see the **Settings** option, you don't have the required permissions\.

![\[The add filter tab, the settings gear in the upper right corner of the page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-custom-attributes-settings.png)

## Search for custom contact attributes<a name="howto-search-for-custom-attributes"></a>

Users who have the **Contact attributes** permission in their security profile can find contacts by using the contact attribute filters\.

1. On the **Contact search** page, choose **Add filter**, **Custom contact attribute**\.

1. In the **Attribute key** box, choose the dropdown to select the key to search\.

1. In the **Attribute values** box, choose value you want to find\. Note that the **Settings** icon doesn't appear in the following image because this user doesn't have **Configure searchable contact attributes** permissions in their security profile\.   
![\[The add filter tab, the attribute values box.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-custom-attributes-search.png)

1. To create a query with multiple custom attributes, choose **Add filter** and **Custom contact attribute** again, and add a different attribute name and specify the value to search for\.

   The following image shows a query that includes two custom attributes: one for **AgentLocation** and another for **InsurancePlanType**\.  
![\[The contact search page, the filters section, two attributes filters.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-custom-attributes-search2.png)