# Access the Customer Profiles Agent UI<a name="customer-profile-access"></a>

After you enable Amazon Connect Customer Profiles, you need to take steps to make the functionality available through the agent user interface\. This topic explains your options\.

## Option 1: Use Customer Profiles with CCP out\-of\-the\-box \(Preview\)<a name="customer-profile-access-out-of-the-box"></a>

In this option, the Customer Profiles widget is already embedded into the CCP\. This option is currently in preview\.

**Note**  
Want to join the preview? [Request access](https://pages.awscloud.com/profiles-agent-app-preview.html)\.  
If your request is approved, your agents will access the CCP and Customer Profiles in the same browser window using a link that looks like this:  
**https://*instance name*\.my\.connect\.aws/agent\-app/**

## Option 2: Embed the Customer Profiles widget into a custom agent experience<a name="customer-profile-access-embed"></a>

When you customize your Contact Control Panel \(CCP\), you have the option of showing or hiding the pre\-built CCP user interface\. For example, you may want to develop a custom agent experience that has a user interface you design, with customized buttons to accept and reject calls\. Or, you may want to embed the pre\-built CCP that's included with Amazon Connect into another custom app\.

Regardless of whether you display the pre\-built CCP user interface, or hide it and build your own, you use the [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) library to embed the CCP and the Customer Profiles widget into the agent's experience\. This way, Amazon Connect Streams is initialized, and the agent can connect and authenticate to Amazon Connect, and Customer Profiles\. 

For information about embedding Customer Profiles, see [Initialization for CCP, Customer Profiles, and Wisdom](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#initialization-for-ccp-customer-profiles-and-wisdom)\.

**Tip**  
When you customize the agent's experience, you determine the URL agents will use to access their agent application, and it might very different from the one provided by Amazon Connect\. For example, your URL could be https://example\-corp\.com/agent\-support\-app\. 