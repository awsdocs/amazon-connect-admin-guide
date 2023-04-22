# Default customer queue: queue hold message and music<a name="default-customer-queue"></a>

This default flow is played when a customer is placed in a queue\. 

1.  The loop has a one\-time voice prompt:

   *Thank you for calling\. Your call is very important to us and will be answered in the order it was received\.*

1. It plays queue music in \.wav format that's been uploaded to the Amazon Connect instance\. 

1. The customer remains in this loop until their call is answered by an agent\.

## Change the default message a customer hears when they are put in queue<a name="change-default-customer-queue"></a>

The following steps show how to change the default message customers hear when they are put in a queue to wait for the next available agent\.

1. On the navigation menu, choose **Routing**, **Flows**\.

1. On the **Contact flows** page, choose **Default customer queue**, as shown in the following image\.  
![\[Default customer queue flow on the contact flows page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customize-default-contact-flow1.png)

1. To customize the message, choose the **Loop prompts** block to open the properties page\.   
![\[Loop prompts block on the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customize-default-contact-flow2.png)

1. Use the dropdown box to either choose different music, or set to **Text to Speech** and then type a message to be played,

   For example, the following image shows the message "*Thank you for calling\. Did you know you can reset your own password at the login page? Choose Reset now, and following the prompts\.*"   
![\[Loop prompts block configured with a text-to-speech message.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customize-default-contact-flow3.png)

1. Choose **Save** at the bottom of the properties page\. 

1. Choose **Publish**\. Amazon Connect starts playing the new message almost immediately \(it may take a few moments for it to fully take effect\)\.  
![\[The publish button on the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customize-default-contact-flow4.png)