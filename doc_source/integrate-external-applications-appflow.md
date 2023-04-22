# Set up integration for external applications using Amazon AppFlow<a name="integrate-external-applications-appflow"></a>

These integrations use Amazon AppFlow to provide periodic updates to Amazon Connect Customer Profiles\. The below steps provide guidance on configuring a connector of your choosing using Amazon AppFlow, configure data mappings, and configure integrations to ingest your customer data\.

For more information on Amazon AppFlow pricing, see Amazon AppFlow [pricing](http://aws.amazon.com/appflow/pricing/)\.

For more information on Amazon AppFlow supported connectors see [Supported source and destination applications](https://docs.aws.amazon.com/appflow/latest/userguide/app-specific.html)\.

## Before you begin<a name="integrate-ea-appflow-pre-req"></a>

When you enable Amazon Connect Customer Profiles you create a Customer Profiles domain, which is a container for all data, such as customer profiles, object types, profile keys, and encryption keys\. The following are guidelines for creating Customer Profile domains:
+ Each Amazon Connect instance can only be associated with one domain\.
+ You can create multiple domains, but they don't share external application integrations or customer data between each other\.
+ All the external application integrations you create are at a domain level\. All of the Amazon Connect instances associated with a domain inherit the domain's integrations\.

**Prerequisite: Enable Customer profiles in your Amazon Connect instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\. The following image shows the **Amazon Connect virtual contact center instances** page, with a box a box around the instance alias\.

1. In the navigation pane, choose **Customer profiles**\.

1. Choose enable Customer Profiles

In the form, you will be required to complete all the mandatory fields to create a Customer Profiles domain by following the steps below:

1. **Domain Setup**\. You can Create New Domain and provide a name\.

1. **Encryption**\. Under Specify KMS key, you can enable encryption by either selecting an existing AWS KMS key, creating a new AWS KMS key, or you can choose **Select existing domain**\.

1. **Error Reporting**\. You can provide a Dead letter queue, which is an SQS queue to handle customer profile errors

1. Choose **Submit** and Customer Profiles will be get created using the Contact History information of your instance\.

### Set up an external application using Amazon AppFlow<a name="integrate-ea-appflow-data-source"></a>

You can add an external application integration to an Amazon Connect Customer Profiles domain by using Amazon AppFlow by following steps below\. You must create a flow for your data source in the Amazon AppFlow console and set Amazon Connect Customer Profiles as the destination prior to continuing in the Customer Profiles console\. If you created a flow more than 14 days ago, it has expired and you will need to create a new flow for your integration\.

You can optionally perform data transformations such as `Arithmetic`, `Filter`, `Map`, `Map_all`, `Mask`, `Merge`, `Truncate`, and `Validate` when using the AWS CloudFormation `AWS::AppFlow::Flow Task` resource prior to ingestion\.

1. Log into your AWS Management Console, select Amazon AppFlow, and choose **Create flow**\.  
![\[The Amazon AppFlow page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step1.png)

1. Enter the flow name and an optional flow description\.  
![\[The Flow details page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step2.png)

1. You can leave the **Data encryption** section as it is since your Amazon Connect Customer Profiles domain already has an existing AWS KMS key that will be used for this Flow\. You can optionally create tags and then choose **Next**\.  
![\[The data encryption section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step3.png)

1. Select an external application of your choice in the **Source name** dropdown and then select the next relevant field\. For example, if you wish to configure Slack, select Slack from the **Source name** dropdown\. You can then either select an existing Slack flow or create a new connection\.  
![\[The configure flow page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step4.png)

1. If you chose to create a new connection, you can then enter the external application's details such as user name, password and subdomain\. You can also select the AWS KMS key for data encryption and enter the connection name to identify this connection\.  
![\[The connect to slack page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step5.png)

1. If you choose to use an existing connection you can select the specific external application object from dropdown\. For example, If choosing an existing Slack connection, you can select **Conversations** as the object and then choose the specific Slack channel that will be used\.  
![\[The source details page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step6.png)

1. In the **Destination details** section, select Amazon Connect as the Destination name in the dropdown and select the Customer profile domain created in the previous prerequisite step\.  
![\[The Destination details section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step7.png)

1. You can select **Run on demand** which runs the flow only when you trigger it\. You also have the option to run the flow at a specific time by setting a schedule\. Choose **Next**\.  
![\[The flow trigger section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step8.png)

1. Choose **Manually map fields** under **Mapping method**\. Choose the source fields from external application and then choose **Map fields directly**\.   
![\[The mapping method section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-create-flow-step9.png)

1. Review and choose **Create flow**\.

For more information on creating flows in the Amazon AppFlow console, see [Creating flows in Amazon AppFlow](https://docs.aws.amazon.com/appflow/latest/userguide/create-flow.html)\.

For more information on the setup of external application and many other supported applications in Amazon AppFlow, see [Supported Amazon AppFlow source and destination applications](https://docs.aws.amazon.com/appflow/latest/userguide/app-specific.html)\.

### Set up data mappings to define how external application data is mapped to a Customer Profile<a name="integrate-ea-appflow-mappings"></a>

Once Amazon AppFlow integration has been set up, you need to set up data mappings in Customer Profiles to define how data from the external application will be mapped to the Customer Profile\. This will allow you to customize the data that you want to use to build your unified customer profile\. Choose your mapping carefully, as you will not be able to choose a different mapping after creating the integration\.

For more detailed information on data mappings, see [Object type mapping](https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-object-type-mapping.html)\.

1. Log into your AWS Management Console, select **Amazon Connect**\. and choose Customer Profiles under your connect instance alias\.  
![\[The Amazon Connect Customer Profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step1.png)

1. Choose **Data mappings** and then choose **Create data mapping**\. Provide a Data Mapping name and a description\.  
![\[The data mapping tab, the create data mapping button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step2.png)  
![\[The set data mapping page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step2_2.png)

1. Under **Mapping options**, you can choose your **Data source** as the external application, the **Flow name** that you created in the previous section, and the **Data definition method** as *Mapping destination*\. Under **Mapping destination** you can choose the types of customer data that wish to define for your unified customer profiles\. Choose **Next**\.  
![\[The mapping options section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step3.png)

1. Add customer, product, case and order attributes with source, destination, and content type, then choose **Next**\.  
![\[The map order attributes page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step4.png)

1. Under **Specify identifiers**, you can select various attributes from your data source object that helps distinguish your data from other data source objects\. You can select attributes from unique, customer, product, case and order identifiers\. For more information about identifiers, see [Standard identifiers](standard-identifiers.md)\.   
![\[The Standard identifiers page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step5.png)

1. Review and choose **Create Data Mapping**\. The Data Mapping status will show as *Active*\.  
![\[Identifiers on the Step 6: Specify identifiers page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-mapping-step6.png)

### Set up integrations to ingest your customer data from an external application<a name="integrate-ea-appflow-integ"></a>

Once the data mapping set up is done for an external application, you will set up the Data source integration to ingest your customer data\. 

1. Log into your AWS Management Console, select **Amazon Connect**\. and choose Customer Profiles under your connect instance alias\.

1. Under the **Data source integrations** section choose **Add data source integration**\.  
![\[Data source integrations tab, add data source integration button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-data-source-integ-step2.png)

1. Under the **Data source** dropdown, select the external application and choose **Next**\. You also have the option to choose **Create new flow** which will open the Amazon AppFlow console in a new tab\.  
![\[Data source section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-data-source-integ-step3.png)

1. Under the **Flow name** dropdown, select the flow you want to use from your data source and choose **Next**\.  
![\[flow name section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-data-source-integ-step4.png)

1. Under the **Data Mapping** dropdown, select the external application data mapping for the object to define how your data source is mapped to profiles\. Choose **Next**\.  
![\[Select data mapping page, mapping dropdown box.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-data-source-integ-step5.png)

1. Review and choose **Add data Source Integration**\. The datasource integration of the external application will initially show as pending before moving to an active state\.  
![\[Review and integrate page, add data source integration button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-ea-data-source-integ-step6.png)

### View the unified customer profile in Amazon Connect Customer Profile Agent CCP<a name="integrate-ea-appflow-view"></a>

Your agents will now be able to view customer data that has been imported from an external application by logging in to the Amazon Connect Agent CCP\. For more information on connecting to the Amazon Connect Agent CCP, see [Agent application: Everything in one place](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-contact-control-panel.html#use-agent-application)\.

Your agent will need to have the appropriate security profile permissions in order to view Customer Profiles and will be able to perform searches using a key name and value in the profiles search bar\.

For more information on security profile permissions, see [Security profiles](https://docs.aws.amazon.com/connect/latest/adminguide/connect-security-profiles.html)\.

Advanced users that wish to build their own custom agent application and embedded customer profiles can use [StreamsJS](http://aws.amazon.com/blogs/https://github.com/amazon-connect/amazon-connect-customer-profiles) which will provide more customization over the agent application\.