# Set up integration for Segment<a name="integrate-customer-profiles-segment"></a>

To provide periodic updates to Amazon Connect Customer Profiles, you can integrate with Segment using Amazon AppFlow\. You first set up the connection in Amazon Connect and Segment, and then verify the Segment integration\.

## Set up the connection in Amazon Connect and Segment<a name="setup-connection-segment"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Customer profiles**\.

1. On the **Customer profiles configuration** page, choose **Add integration**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-addintegration.png)

1. On the **Select source** page, choose **Segment**\. Review the application requirements that are listed on the **Select application** page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-cp-segment-source.png)

1. On the **Establish connection** page, choose one of the following: 
   + **Use existing connection**: This allows you to reuse existing Amazon EventBridge resources that you may have created in your AWS account\.
   + **Create new connection**: Enter the information required by the external application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-segment-establish-connection.png)
     + **Connection name**: Provide a name for your connection\. The connection name is referenced by integrations that use this connection\.
     + **Connection URL**: Enter your application connection URL\. This URL is used for deep\-linking into the objects created in your external application\. The connection URL is the Segment workspace URL available on the application website\. 

       To find your workspace URL:

       1. Log in to your segment\.com account\.

       1. Go to **Settings**, **General settings**\.

       1. Copy the URL from your browser\.
     + **Client ID**: Enter your application client ID\. This is a string that uniquely distinguishes the client in your external application\. This client ID is the Source Name available on the application website\. You use the ID that you specify here to identify the client that you want Customer Profiles to ingest your objects from\. 

       To find your source ID:

       1. Log in to your segment\.com account\.

       1. Go to **Sources**, and choose a source\.

       1. Go to **Settings**, **API Keys**\.

       1. Copy your **Source ID**\.

1. Customer Profiles uses Amazon EventBridge for integrations with Segment\. Log in to your application to continue setting up the Amazon EventBridge event source\. 

1. On the **Source set up** page, copy your AWS account ID to your clipboard, and then choose **Log in to Segment** to configure Amazon EventBridge\. 

1. Use the following instructions to set up Segment:

   1. Log in to Segment\.

   1. In your application, select a source to set up the destination to Customer Profiles\.

   1. Paste in your AWS account ID and select your AWS Region\.

   1. Toggle **ON**, to activate your partner event source\.

   1. Go to **Event Tester**, and send a test event to complete activating your partner event source\.

   1. After you set up the event source destination, return to Customer Profiles\. You will see an alert that indicates Amazon Connect has successfully connected with Segment\.

1. On the **Integration options** page, choose which source objects you want to ingest and select their object type\. 

   Object types store your ingested data\. They also define how objects from your integrations are mapped to profiles when they are ingested\. Customer Profiles provides default object type templates you can use that define how attributes in your source objects are mapped to the standard objects in Customer Profiles\. You can also use the object mappings that you've created from the [PutProfileObjectType](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutProfileObjectType.html)\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-integration-options-segment.png)

1. For the **Ingestion start date**, Customer Profiles starts ingesting records created after the integration is added\. 
**Note**  
If you need historical records, you can [use Amazon S3 as an integration source to import them](customer-profiles-object-type-mappings.md)\. 

1. On the **Review and integrate** page, check that the **Connection status** says **Connected**, and then choose **Add integration**\. 

1. After the integration is set up, back on the **Customer profiles configuration** page, the **Integrations** page displays which integrations are currently set up\. The **Last run ** and **Integration health** are not currently available for this type of integration\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-shopify-integrations-view-card.png)

   To see what data is being sent, choose the integration and\+ then choose **View objects **\.

## Verify your Segment integration<a name="verify-customer-profile-segment-connection"></a>

To perform this step you need the following prerequisites: 
+ Access to your Segment workspace\.
+ [Access to the Amazon Connect Contact Control Panel](amazon-connect-contact-control-panel.md)\.

**To verify your Segment integration**

1. Go to your Segment workspace dashboard and choose **Destinations**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-segment-1.png)

1. You will see a list of destinations where that Segment sends data\. Choose the EventBridge destination for Customer Profiles\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-segment-2.png)

1. Choose the **Event Tester** tab\. From this page you will send a test event to Customer Profiles\. The event is ingested and turned into a customer profile that you can view in the Amazon Connect agent application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-segment-3.png)

1. Select **Identify** as the event type, and select **Event Builder** as your input method\.

1. You can specify a **User ID** and some traits\. Agents can search for these traits in the agent application\. 

1. Choose **Send Event**\.

1. The event delivery should be almost instantaneous but allow it a minute for it to be delivered and create a customer profile\.

1. Open the Amazon Connect agent application\. Search for the user ID you entered in the **Event Builder**\. You should be able to see the customer profile with the user ID and the traits you entered\.

1. If you cannot see the customer profile, then there is a problem with your integration\. To troubleshoot:

   1. Go to the Amazon EventBridge console\. 

   1. Check whether the EventSource is Active and the matching EventBus exists and is running\.

   If these are working, contact AWS Support for assistance investigating the issue\.

## Monitor your Customer Profiles integrations<a name="monitor-customer-profile-connection-segment"></a>

After your connection is established, if it stops working, delete the integration and then re\-establish it\. 

## What to do if objects aren't being sent<a name="fix-customer-profile-connection-segment"></a>

If an object fails to be sent, choose **Flow details** to learn more about what's gone wrong\. 

You may need to delete the configuration and re\-connect to the external application\. 