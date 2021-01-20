# Integrate external applications with Customer Profiles<a name="integrate-external-apps-customer-profiles"></a>

Amazon Connect provides a set of pre\-built integrations powered by Amazon AppFlow\. After you enable Amazon Connect Customer Profiles, you can use these integrations to combine information from external applications such as Salesforce or Zendesk, with contact history from Amazon Connect\. This creates a customer profile that has all the information agents need during customer interactions in a single place\.

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Customer profiles**\.

1. On the **Customer profiles configuration** page, choose **Add integration**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-addintegration.png)

1. On the **Select application** page, choose which external application you want to get customer profiles data from\. Select **Read and acknowledge** to indicate you understand the connection requirements for your application\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-choose-app.png)

1. On the **Establish connection** page, choose one of the following: 
   + **Use existing connection**: This allows you to reuse existing Amazon AppFlow resources you may have created in your AWS account\.\.
   + **Create new connection**: Enter the information required by the external application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-establish-connection.png)

1. On the **Review and integrate** page, check that the **Connection status** says **Connected**, and then choose **Create integration**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-review-and-integrate.png)

1. After the integration is set up, back on the **Customer profiles configuration** page, choose **View objects** to see what data is being batched and sent\. Currently, this process ingests records that were created or modified in the last 30 days\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-objects.png)

## Monitor your Customer Profile integrations<a name="monitor-customer-profile-connection"></a>

After your connection is established, if it stops working, delete the integration and then re\-establish it\. 

## What to do if objects aren't being sent<a name="fix-customer-profile-connection"></a>

If an object fails to be sent, choose **Flow details** to learn more about what's gone wrong\. 

You may need to delete the configuration and re\-connect to the external application\. 

## Delete/stop Customer Profile integrations<a name="delete-customer-profile-connection"></a>

If at any time you want to stop the ingestion of customer profile data, choose the application and then choose **Delete**\. 
+ To delete customer profiles data for a specific integration, use the `DeleteObjectType` API\.
+ To delete the integrations, customer profiles, and all the customer profile data, use the `DeleteDomain` API\.

To re\-enable the ingestion of customer profile data, go through the setup steps again\. 