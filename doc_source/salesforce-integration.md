# Amazon Connect and Salesforce Integration<a name="salesforce-integration"></a>

The Amazon Connect CTI Adapter provides a WebRTC browser\-based Contact Control Panel \(CCP\) within Salesforce\. This integration enables your agents to leverage both inbound caller ID screen pop and outbound click to call/transfer/conferencing\.

We recommend that you initially install the package into your Salesforce sandbox\. After the package is installed, you can configure your Salesforce Call Center configuration within Salesforce\. This configuration is a XML file that you import into your call center\. It provides all the details required to enable the CTI\.

The next step is to whitelist your Salesforce Visualforce domain within your Amazon Connect Application integration\. This allows cross\-domain access to your Amazon Connect instance\.

**Prerequisites**

+ Salesforce Classic, Salesforce Console, or Lightning Experience

+ An Amazon Connect instance with a user account assigned only the Agent security role\. The user accounts for Salesforce and Amazon Connect are separate accounts\. You should log in to Amazon Connect with your user account that is assigned the Agent security role\. You should also log in to Salesforce using a Salesforce user account that has been granted access to the CCP in Salesforce\. 

  For information about how to assign security profiles, see the [Amazon Connect User Guide](http://docs.aws.amazon.com/connect/latest/userguide/)

+ A Firefox or Chrome browser

**To integrate with Salesforce**

1. In your Salesforce sandbox, install the following managed package: [Amazon Connect CTI Adapter](https://appexchange.salesforce.com/listingDetail?listingId=a0N3A00000EJH4yUAH)\.

1. Edit the call center configuration as follows:

   + For **CTI Adapter URL**, type the one of the following, based on your Salesforce interface:

     + **/apex/amazonconnect\_\_ACSFCCP\_Classic**

     + **/apex/amazonconnect\_\_ACSFCCP\_Console**

     + **/apex/amazonconnect\_\_ACSFCCP\_Lightning**

   + For **Salesforce Compatibility Mode**, choose **Classic** for the Salesforce Classic and Salesforce Console or **Lightning** for Lightning Experience\.

   + For **Amazon Connect CCP URL**, type the CCP URL for your instance \(for example, https://*instance*\.awsapps\.com/connect/ccp\)\.

   + For **Phone Number Formatting**, **Country**, specify the appropriate 2\-digit [ISO country code](https://countrycode.org/)\.

   + To provide Salesforce users with access to the Amazon Connect CCP, on the **Setup Call Centers** page, choose **Manage Call Center Users**\. Add the Salesforce users you want to enable for using these call features\. Be sure to add your own Salesforce user account if you plan to these features\.

1. Whitelist your Salesforce Visualforce domain URL using the directions in [Application Integration](amazon-connect-instance.md#app-integration)\. This URL usually has the following format:

   ```
   https://amazonconnect.instance.visual.force.com
   ```

   To verify the URL, open the Visualforce page in setup\.

1. Log in to your Amazon Connect instance\.

1. Launch Salesforce\. You should see the integrated CCP in the side panel \(Salesforce Classic\) or the phone toolbar \(Salesforce Classic and Lightning Experience\)\.

## Troubleshooting Common Issues<a name="troubleshooting"></a>

If you encounter errors with your configuration, check the following common issues:

+ Confirm that Salesforce is not blocking your iFrame\. For more information, see [ Enable Clickjack Protection for Visualforce Pages Even When Headers Are Disabled](https://releasenotes.docs.salesforce.com/en-us/summer15/release-notes/rn_vf_clickjack_with_headers_disabled.htm)\.

+ Confirm that the Amazon Connect user is assigned only the Agent security profile\.

+ Confirm that your Salesforce Call Center **Phone Number Formatting** is configured with the following parameters:

  \{"OPF":"0","NPF”:"*2 digit dialing code*","Country”:"*2 digit country code*","NF":"International\_plaintext","TNF":"\(555\) 123\-4567"\}

+ Confirm that the Salesforce user can access the call center\. To check a user's status, choose **Manage Call Center Users**\.

+ Under **Softphone Layout**, **Screen Pop**, confirm that **Single\-matching record** is set to **Pop detail page** and **Multiple\-matching record** is set to **Pop to search page**\.

+ If you are using Salesforce Lightning Experience and do not see a phone toolbar icon, confirm that you have enabled console navigation\. To enable console navigation, in the **Salesforce Setup Console**, choose **App Manager**, **Service Console \(Lightning\)**, **Edit**\. On the **Edit** page, choose **App Options**, **App Navigation**, **Console Navigation**\.