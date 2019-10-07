# Amazon Connect and Salesforce Integration<a name="salesforce-integration"></a>

The core functionality of the Amazon Connect CTI Adapter provides a WebRTC browser\-based Contact Control Panel \(CCP\) within Salesforce\. The Amazon Connect CTI integration consists of two components: 
+ A managed Salesforce package\.
+ An AWS Serverless application deployed to your AWS environment\.

With those components, you can build a deep integration between the Amazon Connect contact center platform and Salesforce, the leading customer relationship management \(CRM\) platform\. The collection of pre\-build utilities enables a rapid integration between these two platforms\. The AWS Serverless application package contains a set of common Lambda functions to be used by Amazon Connect to interact with Salesforce\.

## About the Adapter<a name="adapter-v2"></a>

The key benefits of the adapter include:
+ Agent state synchronization between Salesforce Omni and Amazon Connect
+ Provide valuable information to the agent through configurable view of call attributes
+ Utilize the Amazon Connect Call Campaign Object for automated outbound dialling
+ Automatically create phone call tasks and relate it to the right Salesforce object
+ Embed Amazon Connect Call Recordings in the Salesforce record
+ Automatically clean\-up open tabs to improve agent efficiency
+ Easily enable lookup, create and update operations for different Salesforce objects, like Contacts and Cases, within Amazon Connect contact flows\.
+ Support Salesforce Sales and Service Console in Classic and Lightning\.

We recommend that you initially install the package into your Salesforce sandbox\. After the package is installed, you can configure your Salesforce Call Center configuration within Salesforce\.

The next step is to whitelist your Salesforce Visualforce domain within Amazon Connect\. This allows cross\-domain access to your Amazon Connect instance\.

## Amazon Connect CTI Adapter v3 for Salesforce Installation Guide<a name="sf-installation-guide"></a>

For a detailed walk\-through and setup of the full CTI Adapter capabilities, see the [Amazon Connect CTI Adapter v3 for Salesforce installation guide](https://s3.amazonaws.com/connect-blogs/Amazon+Connect+Salesforce+CTI+Adapter/Amazon+Connect+CTI+Adapter+-+Setup+and+Installation+Guide.pdf)\. We also have a trailhead available at [https://sfdc\.co/Amazon\-Connect](https://sfdc.co/Amazon-Connect)\. Note, it's still in process of being updated to support latest CTI Adapter features\.

## Prerequisites<a name="v2-prereqs"></a>

Before the Amazon Connect CTI package can be installed, the following prerequisites need to be fulfilled:
+ Salesforce Classic, Salesforce Console, or Lightning Experience
+ Create an Amazon Connect instance \([https://aws\.amazon\.com/connect/](https://aws.amazon.com/connect/)\)\.
+ Salesforce Omni\-Channel must be activated in the Salesforce org\. For more information, see [Enable Omni\-Channel](https://help.salesforce.com/articleView?id=omnichannel_enable.htm)\. 

## Browser Compatibility<a name="v2-browsers"></a>

Amazon Connect requires WebRTC to enable soft\-phone voice media stream and Websockets to enable soft\-phone signalling\. Consequently, users are required to use the latest version of either Google Chrome or Mozilla Firefox\. For more details, please see the [Amazon Connect FAQ](https://aws.amazon.com/connect/faqs/) page\.

## Quick Setup for a Sandbox Environment<a name="integrate-v2"></a>

1. In your Salesforce sandbox, install the following managed package: [Amazon Connect CTI Adapter](https://appexchange.salesforce.com/listingDetail?listingId=a0N3A00000EJH4yUAH)\.

1. Edit one of appropriate call center configuration \(Amazon Connect CCP Adapter Classic, Console, or Lightning\)\.
   + For Amazon Connect CCP URL, type the CCP URL for your instance \(for example, https://instance\.awsapps\.com/connect/ccp\)\.
   + For Phone Number Formatting, Country, specify the appropriate 2\-digit [ISO country code](https://countrycode.org/)\.
   + To provide Salesforce users with access to the Amazon Connect CCP, on the Setup Call Centers page, choose **Manage Call Center Users**\. Add the Salesforce users to enable for using these call features\. Be sure to add your own Salesforce user account if you plan to these features\.

1. Whitelist your Salesforce Visualforce domain URL using the directions in [Use an Allow List for Integrated Applications](app-integration.md)\. To verify the URL, open the Visualforce page in setup\. This URL usually has the following format:

   https://amazonconnect\.**your\-instance\-name**\.visual\.force\.com

1. Log in to your Amazon Connect instance\.

1. Launch Salesforce\. You should see the integrated CCP in the side panel \(Salesforce Classic\) or the phone toolbar \(Salesforce Classic and Lightning Experience\)\.

## Known Issue<a name="sf-known-issues"></a>

Upon the completion of a call, Amazon Connect puts the agent into the After Contact Work state\. As part of the Adapter, a Call Wrap\-Up page will be triggered in Salesforce\. When you integrate Amazon Connect with Saleforce Classic, this page will be not be triggered\. 

## Troubleshooting Common Issues<a name="troubleshooting-crm"></a>

If you encounter errors with your configuration, check the following common issues:
+ Confirm that Salesforce is not blocking your iFrame\. For more information, see [Enable Clickjack Protection for Visualforce Pages Even When Headers Are Disabled](https://releasenotes.docs.salesforce.com/en-us/summer15/release-notes/rn_vf_clickjack_with_headers_disabled.htm)\.
+ Confirm that the Amazon Connect user is assigned only the Agent security profile\.
+ Confirm that your Salesforce Call Center **Phone Number Formatting** is configured with the following parameters:

  \{"OPF":"0","NPF”:"*2 digit dialing code*","Country”:"*2 digit country code*","NF":"International\_plaintext","TNF":"\(555\) 123\-4567"\}
+ Confirm that the Salesforce user can access the call center\. To check a user's status, choose **Manage Call Center Users**\.
+ Under **Softphone Layout**, **Screen Pop**, confirm that **Single\-matching record** is set to **Pop detail page** and **Multiple\-matching record** is set to **Pop to search page**\.
+ If you are using Salesforce Lightning Experience and do not see a phone toolbar icon, confirm that you have enabled console navigation\. To enable console navigation, in the **Salesforce Setup Console**, choose **App Manager**, **Service Console \(Lightning\)**, **Edit**\. On the **Edit** page, choose **App Options**, **App Navigation**, **Console Navigation**\.