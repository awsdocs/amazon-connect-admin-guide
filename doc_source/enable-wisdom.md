# Enable Amazon Connect Wisdom for your instance<a name="enable-wisdom"></a>



There are two ways you can enable Wisdom for your instance: 
+ Use the [new](amazon-connect-release-notes.md#august21-release-notes) Amazon Connect console\. This topic provides instructions\.
+ Use the Amazon Connect Wisdom API\. You can ingest content using the Amazon Connect Wisdom APIs\. To learn more, see this blog post: [Ingesting content to power real\-time recommendations and search with Amazon Connect Wisdom](http://aws.amazon.com/blogs/contact-center/ingesting-content-to-power-real-time-recommendations-and-search-with-amazon-connect-wisdom/)\. 

  The APIs support the ingestion of HTML and text; plain text files must be in UTF\-8\. For more information, see the [Amazon Connect Wisdom API Reference](https://docs.aws.amazon.com/wisdom/latest/APIReference/)\. 

Following is an overview of the steps to enable Wisdom:

1. Create a Wisdom Assistant \(domain\)\. An Assistant is made up of one knowledge base\.

1. Create an encryption key to encrypt the excerpt that is provided in the recommendations to the agent\.

1. Create a knowledge base using external data:
   + Add data integrations from [ Salesforce](https://developer.salesforce.com/docs/atlas.en-us.knowledge_dev.meta/knowledge_dev/sforce_api_objects_knowledge__kav.htm) and [ ServiceNow](https://developer.servicenow.com/dev.do#!/reference/api/rome/rest/knowledge-management-api) using prebuilt connectors in the Amazon Connect console\.
   + Encrypt the content importing from these applications using a KMS key\.
   + Specify the sync frequency\.

## Before you begin<a name="enable-wisdom-requirements"></a>

Following is an overview of key concepts and the information that you'll be prompted for during the setup process\. 

### About the Wisdom domain<a name="wisdom-domain"></a>

When you enable Amazon Connect Wisdom, you create a Wisdom domain: an Assistant that is made up of one knowledge base\. Following are guidelines for creating Wisdom domains: 
+ Each Amazon Connect instance can only be associated with one domain\. 
+ You can create multiple domains, but they don't share external application integrations or customer data between each other\. 
+ All the external application integrations you create are at a domain level\. All of the Amazon Connect instances associated with a domain inherit the domain's integrations\. 
+ You can change the association of your Amazon Connect instance from your current domain to a new domain at any time, by choosing a different domain\. 

### How do you want to name your Wisdom domain?<a name="enable-wisdom-domains"></a>

When you enable Wisdom, you are prompted to provide a friendly domain name that's meaningful to you such as your organization name, for example, *Wisdom\-ExampleCorp*\. 

### Create AWS KMS keys to encrypt the domain and the connection<a name="enable-wisdom-awsmanagedkey"></a>

 When you enable Wisdom, by default the domain and connection are encrypted with an AWS owned key\. However, you have the option to create or provide two [AWS KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#kms_keys):

1. One for the Wisdom domain, used to encrypt the excerpt provided in the recommendations\. 

1. Another to encrypt the content imported from Salesforce and ServiceNow\. Note that Wisdom search indices are always encrypted at rest using an AWS owned key\.

Step\-by\-step instructions for creating these KMS keys are provided in [Step 1: Add integration](#enable-wisdom-step1)\.

Your customer managed key is created, owned, and managed by you\. You have full control over the KMS key \(AWS KMS charges apply\)\.

If you choose to set up a KMS key where someone else is the administrator, the key must have a policy that allows `kms:CreateGrant` and `kms:DescribeKey` permissions to the IAM identity using the key to invoke Wisdom\. For information about how to change a key policy, see [Changing a key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html) in the AWS Key Management Service Developer Guide\.

**Tip**  
You can create KMS keys or provide an existing KMS key programmatically\. For more information, see 

## Step 1: Add integration<a name="enable-wisdom-step1"></a>

Following are instructions for how to create a new domain and add an integration\.

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Wisdom**, and then choose **Add domain**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-page.png)

1. On the **Add domain** page, choose **Create a domain**\.

1. In the **Domain name** box, enter a friendly name that's meaningful to you, such as your organization name, for example, *Wisdom\-ExampleCorp*\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-enable-domain.png)

1. Under **Encryption**, create or enter your own AWS KMS key for encrypting your Wisdom domain\. Following are the steps to create your KMS key:

   1. On the **Add domain** page, choose **Create an AWS KMS key**\.

   1. A new tab in your browser opens for the Key Management Service \(KMS\) console\. On the **Configure key** page, choose **Symmetric**, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-configure-key.png)

   1. On the **Add labels** page, add a name and description for the KMS key, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-add-labels.png)

   1. On the **Define key administrative permissions** page, choose **Next**\.

   1. On the **Define key usage permissions** page, choose **Next**\.

   1. On the **Review and edit key policy** page, choose **Finish**\.

      In the following example, the name of the KMS key starts with **bcb6fdd**:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-note-key.png)

   1. Return to the tab in your browser for the Amazon Connect console, **Wisdom** page\. Click or tap in the **AWS KMS key** for the key you created to appear in a dropdown list\. Choose the key you created\.

1. Choose **Add domain**\. 

1. On the **Wisdom** page, choose **Add integration**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-add-integration.png)

1. On the **Add integration** page, choose **Create a new integration**, and then select the source\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-select-integration.png)

1. In the **Integration name** box, assign a friendly name to the integration, one that is meaningful to you\. 
**Tip**  
If you are going to have mutiple integrations from the same source, we recommend you develop a naming convention to make them easy to distinguish\.

1. Under **Connection with \[Source\]**, choose **Create a new connection**, and then enter a friendly name for the connection that is meaningful to you\.

1. Enter the instance URL of the source you want to connect to, and then choose **Log in to \[Source\]**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-connection-url.png)

1. Under **Encryption**, choose **Create an AWS KMS key**\. This key encrypts the connection to the external application that stores content\. Following are the steps to create your KMS key:

   1. On the **Add domain** page, choose **Create an AWS KMS key**\.

   1. A new tab in your browser opens for the Key Management Service \(KMS\) console\. On the **Configure key** page, choose **Symmetric**, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-configure-key.png)

   1. On the **Add labels** page, add a name and description for the KMS key, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-add-labels.png)

   1. On the **Define key administrative permissions** page, choose **Next**\.

   1. On the **Define key usage permissions** page, choose **Next**\.

   1. On the **Review and edit key policy** page, choose **Finish**\.

      In the following example, the name of the KMS key starts with **bcb6fdd**:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-note-key.png)

   1. Return to the tab in your browser for the Amazon Connect console, **Wisdom** page\. Click or tap in the **AWS KMS key** for the key you created to appear in a dropdown list\. Choose the key you created\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-encrypt-connection.png)

1. Under **Ingestion start date**, choose when you want Wisdom to import records from your application, and how often\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-ingestion-start-date.png)

   1. Defaults to the earliest date possible\.

1. Under **Sync frequency**, the default is hourly\. You can use the dropdown to choose **Every 3 hours** or **Daily**\. On\-demand syncing is not available\.

1. Choose **Next**\.

**Note**  
Currently Wisdom does not process hard deletes of objects that are completed in SaaS applications\. To remove content from your knowledge base that's also been removed from your SaaS application, you must archive objects in Salesforce and retire articles in ServiceNow\.

## Step 2: Select object and fields<a name="enable-wisdom-step2"></a>

In this step you choose the object and fields from the source that you want to make available to your agents in Wisdom\.

1. In the **Available objects** dropdown menu, choose the object you want\. Only knowledge objects appear in the menu\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-select-objects.png)

1. Under **Select Fields for \[object name\]**, choose the fields you want to include\. You'll notice that some fields, such as **AccountID** and **ID**, are already selected by default\. These fields are required\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-select-fields.png)

1. Choose **Next**\.

## Step 3: Review and integrate<a name="enable-wisdom-step3"></a>

1. Review all the integration details\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-review-uri-template.png)
**Note**  
The URI template is based on your version of Salesforce \(such as Lightning\), and the object you chose\. You may want to change it if, for example, you're on a different version of Salesforce, or you have a connector that has a different desktop client\.

1. Choose **Add integration**\.

1. The integration is added to your list, as shown in the following example\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-integration-added.png)

1. After an integration is created, you can edit the URI, but no other information\.

## Step 4: Add a Wisdom block to your contact flow<a name="enable-wisdom-step4"></a>

By adding a [Wisdom](wisdom.md) block to your contact flow, you associate a Wisdom domain to the current contact\. This enables you to display information from a specific domain, based on criteria about the contact\.

**Note**  
Amazon Connect Wisdom, along with Contact Lens Real\-Time analytics, is used to recommend content that is related to customer issues detected during the current contact\. The [Set recording and analytics behavior](set-recording-behavior.md) block with Contact Lens real\-time enabled must also be set in this flow for Wisdom recommendations to work\. It doesn’t matter where in the flow you add [Set recording and analytics behavior](set-recording-behavior.md)\. 

## When was your knowledge base last updated?<a name="enable-wisdom-tips"></a>

To confirm the last date and time that your knowledge base was updated \(meaning a change in the content available\), use the [GetKnowledgeBase](https://docs.aws.amazon.com/wisdom/latest/APIReference/API_GetKnowledgeBase.html) API to reference `lastContentModificationTime`\.