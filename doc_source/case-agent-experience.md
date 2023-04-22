# Access Cases in the agent application<a name="case-agent-experience"></a>

After you enable Amazon Connect Cases, you need to take steps to make the functionality available through the agent application\. This topic explains your options\.

**Tip**  
Make sure your agents have **Cases** permissions in their security profile so they can access Cases\. For more information, see [Security profile permissions for Cases](assign-security-profile-cases.md)\.

## Option 1: Use Cases with the CCP out\-of\-the\-box<a name="cases-access-out-of-the-box"></a>

Cases is already embedded alongside the Contact Control Panel \(CCP\)\. Your agents will access the CCP and Cases in the same browser window using a link that looks like this:
+ **https://*instance name*\.my\.connect\.aws/agent\-app\-v2/** 

If you access your instance using the **awsapps\.com** domain, use the following URL: 
+ **https://*instance name*\.awsapps\.com/connect/agent\-app\-v2/**

For help finding your instance name, see [Find your Amazon Connect instance name](find-instance-name.md)\.

## Option 2: Embed Cases into a custom agent application<a name="cases-access-embed"></a>

When you embed your Contact Control Panel \(CCP\), you have the option of showing or hiding the pre\-built CCP user interface\. For example, you may want to develop a custom agent application that has a user interface you design, with customized buttons to accept and reject calls\. Or, you may want to embed the pre\-built CCP that's included with Amazon Connect into another custom app\.

 You can display the pre\-built CCP user interface, or hide it and build your own\. In both scenarios, you can incorporate Cases into your agent application by using public APIs provided by Amazon Connect\. These APIs are built to provide you the flexibility to create the functionality and user experience that you want\. For more information, see the [Cases API documentation](https://docs.aws.amazon.com/cases/latest/APIReference/Welcome.html)\. 

**Tip**  
When you customize the agent's application, you determine what URL agents will use to access their agent application\. This might be very different from the one provided by Amazon Connect\. For example, your URL could be https://example\-corp\.com/agent\-support\-app\. 