# Enable outbound calls<a name="enable-outbound-calls"></a>

Before your agents can make outbound calls to customers, you need to set up your Amazon Connect instance for outbound communications\.

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Telephony**\.

1. To enable outbound calling from your contact center, choose **Make outbound calls with Amazon Connect**\.

1. To enable outbound campaigns, choose **Enable outbound campaigns**\.

1. By enabling early media audio, your agents can hear pre\-connection audio such as busy signals, failure\-to\-connect errors, or other informational messages from telephony providers, when making outbound calls\. Choose **Enable early media**\.

1. Choose **Save**\.

**Note**  
For a list of countries you can call **by default** based on the Region of your instance, see [Countries you can call by default](country-code-allow-list.md)\.  
For a list of all countries available for outbound calls based on the Region of your instance, see [Amazon Connect pricing](http://aws.amazon.com/connect/pricing/)\. If a country is not available in your dropdown menu, open a ticket to add it to your allow list\. 