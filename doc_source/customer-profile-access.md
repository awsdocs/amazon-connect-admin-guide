# Access Customer Profiles in the agent application<a name="customer-profile-access"></a>

After you enable Amazon Connect Customer Profiles, you need to take steps to make the functionality available through the agent application\. This topic explains your options\.

**Tip**  
Make sure your agents have **Customer profiles** permissions in their security profile so they can access Customer Profiles\. For more information, see [Security profile permissions for Customer Profiles](assign-security-profile-customer-profile.md)\.

## Option 1: Use Customer Profiles with the CCP out\-of\-the\-box \(Preview\)<a name="customer-profile-access-out-of-the-box"></a>

Customer Profiles is already embedded alongside the Contact Control Panel \(CCP\)\. Your agents will access the CCP and Customer Profiles in the same browser window using a link that looks like this:
+ **https://*instance name*\.my\.connect\.aws/agent\-app\-v2/** 

If you access your instance using the **awsapps\.com** domain, use the following URL: 
+ **https://*instance name*\.awsapps\.com/connect/agent\-app\-v2/**

For help finding your instance name, see [Find your Amazon Connect instance name](find-instance-name.md)\.

Following is an example of what the CCP and Customer Profiles look like in the same browser window\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-agent-app.png)

## Option 2: Embed Customer Profiles into a custom agent application<a name="customer-profile-access-embed"></a>

When you embed your Contact Control Panel \(CCP\), you have the option of showing or hiding the pre\-built CCP user interface\. For example, you may want to develop a custom agent application that has a user interface you design, with customized buttons to accept and reject calls\. Or, you may want to embed the pre\-built CCP that's included with Amazon Connect into another custom app\.

Regardless of whether you display the pre\-built CCP user interface, or hide it and build your own, you use the [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) library to embed the CCP and Customer Profiles into the agent's application\. This way, Amazon Connect Streams is initialized, and the agent can connect and authenticate to Amazon Connect, and Customer Profiles\. 

For information about embedding Customer Profiles, see [Initialization for CCP, Customer Profiles, and Wisdom](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#initialization-for-ccp-customer-profiles-and-wisdom)\.

**Tip**  
When you customize the agent's application, you determine the URL agents will use to access their agent application, and it might very different from the one provided by Amazon Connect\. For example, your URL could be https://example\-corp\.com/agent\-support\-app\. 