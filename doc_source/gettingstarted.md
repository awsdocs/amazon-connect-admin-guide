# Getting Started with Amazon Connect<a name="gettingstarted"></a>

An Amazon Connect instance is the starting point for your contact center\. After you create an instance, you can edit the settings for it, which include telephony, data storage, data streaming, application integration, and contact flows\. You can then launch your instance from the AWS Management Console and start using your contact center\.

**Note**  
Amazon Connect is not available to customers in India using Amazon Web Services through Amazon Internet Services Pvt\. Ltd \(AISPL\)\. You will receive an error message if you try to create an instance in Amazon Connect\.

After you create an Amazon Connect instance, you can claim a phone number to use for your contact center\. After you claim a number, you can place a test call in to your contact center to confirm that it is working correctly\. Calls are handled in the contact center using the Contact Control Panel \(CCP\)\. The CCP is built in to the Amazon Connect Contact Center Manager \(CCM\)\. For more information about how agents use the CCP, see [Using the Contact Control Panel](https://docs.aws.amazon.com/connect/latest/userguide/agentconsole.html) in the *Amazon Connect User Guide*\.

You can edit the settings for your instance in the AWS Management Console\. After you create your instance, you can access it by using the URL in the **Access URL** column\. The access URL is the URL your agents, administrators, and managers use to log in to and access the CCM and the CCP\. For more information, see [Amazon Connect Instances](what-is-amazon-connect.md#amazon-connect-fundamentals)\.

**Note**  
If you use SAML\-based authentication for identity management, your users must log in to your instance through your identity provider instead of using the access URL for your instance\.

## Before You Begin<a name="prerequisites"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Amazon Connect\. You are charged only for the services that you use\.

If you have an AWS account already, skip to the next task\. If you don't have an AWS account, use the following procedure to create one\.

**To create an AWS account**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.
**Note**  
If you previously signed in to the AWS Management Console using AWS account root user credentials, choose **Sign in to a different account**\. If you previously signed in to the console using IAM credentials, choose **Sign\-in using root account credentials**\. Then choose **Create a new AWS account**\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code using the phone keypad\.

### Port and Protocol Requirements<a name="connect-ports-protocols"></a>

If you plan to use the Amazon Connect softphone Contact Control Panel \(CCP\) for your agents to handle calls in Amazon Connect, you need allow traffic through the ports for the required protocols used by Amazon Connect to communicate with the softphone and other AWS services used by Amazon Connect\. The softphone client runs in a web browser, and connects to Amazon Connect and other AWS services using a set of public IP addresses and TCP/UDP ports\. To allow for that communication, you must permit traffic in your network to the ports and protocols described in [Softphone CCP IP Address Ranges](https://docs.aws.amazon.com/connect/latest/userguide/agentconsole-guide.html#ccp-ip-ranges)\.

## Plan for User and Identity Management<a name="identity-management"></a>

Before you set up your Amazon Connect instance, you should decide how you want to manage your Amazon Connect users\. You cannot change the option you select for identity management after you create the instance\. If you decide to change the option or directory you selected, you can delete the instance and create a new one\. When you delete an instance, you lose all configuration settings and metrics data for it\.

You can choose from one of the following supported identity management solutions supported in Amazon Connect:
+ **Store users with Amazon Connect**—Choose this option if you want to create and manage user accounts within Amazon Connect\. When you manage users in Amazon Connect, the user name and password for each user is specific to Amazon Connect\. Users must remember a separate user name and password to log in to Amazon Connect\.
+ **Link to an existing directory**—Choose this option to use an existing directory\. The directory must be associated with your account, set up in AWS Directory Service, and be active in the same Region in which you create your instance\. If you plan to choose this option, you should prepare your directory before you create your Amazon Connect instance\. For more information, see [Use an Existing Directory for Amazon Connect Identity Management](directory-service.md)\.
+ **SAML 2\.0\-based authentication**—Choose this option if you want to use your existing network identity provider to federate users with Amazon Connect\. Users can only log in to Amazon Connect by using the link configured through your identity provider\. If you plan to choose this option, you should configure your environment for SAML before you create your Amazon Connect instance\. For more information, see [Configure SAML for Identity Management in Amazon Connect](configure-saml.md)\.

## Create an Amazon Connect Instance<a name="launch-contact-center"></a>

You can create or add an instance as follows\.

**To create an Amazon Connect instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Do one of the following:
   + If you have not previously created an Amazon Connect instance, choose **Get started**\.
   + If you have previously created an instance, choose **Add an instance**\.

1. For **Step 1: Identity management** step, do one of the following:
   + To manage your users within Amazon Connect, choose **Store users within Amazon Connect**\.
   + To use an existing directory where your users are managed, choose **Link to an existing directory**\. For more information about using an existing directory, see [Use an Existing Directory for Amazon Connect Identity Management](directory-service.md)\.
   + To use SAML\-based authentication with your identity provider to federate users with Amazon Connect, choose **SAML 2\.0\-based authentication**\. For more information about using SAML with Amazon Connect, see [Configure SAML for Identity Management in Amazon Connect](configure-saml.md)\.

1. For **Access URL**, enter an instance alias for your instance, and choose **Next step**\.

   The name that you enter is displayed as the instance alias in the AWS Management Console, and is used as the domain in the access URL to access your contact center\. The alias must be globally unique, meaning that an alias can be used only one time across all Amazon Connect instances and Regions\. You cannot change the alias URL after your instance is created\.

1. For **Step 2: Administrator**, do one of the following:
   + If you chose **Store users with Amazon Connect** for identity management, enter the user details for an admin account, and choose **Next step**\.
   + If you chose **Link to an existing directory** for identity management, enter the user name for the account to use as the admin account for your instance, and choose **Next step**\.

     If the user name that you enter does not exist in your directory, you can add it later\.
   + Choose **Skip this** to create an admin account later\. To create an admin later, log in to your instance as an administrator from the Amazon Connect console\.

1. For **Step 3: Telephony options**, indicate whether you'd like your contact center to accept calls, make calls, or both\. You can set the user permissions within the Amazon Connect web application\. The telephone number options are provided after setup\.

1. For **Step 4: Data storage**, you can keep the default settings or choose **Customize settings**\. For more information, see [Data Storage](amazon-connect-instance.md#datastorage)\.

1. For **Step 5: Review and create**, review your settings and choose **Create instance**\.
**Important**  
This is the only time you can change the directory and domain name settings—you can edit any other setting later on\.

1. After your instance is created, choose **Get started** to claim and test a phone number\. Amazon Connect automatically configures your instance to use the phone number that you select\.
**Note**  
For information about how to keep your current phone number and use it with Amazon Connect, see [Port Your Current Phone Number](#numberporting)\.

1. \(Optional\) Continue to configure your instance\. For more information, see [Configuring Your Amazon Connect Instance](amazon-connect-instance.md)\.

## Port Your Current Phone Number<a name="numberporting"></a>

To continue to use your current United States phone number with Amazon Connect, you can submit a support ticket to port the number to Amazon Connect\. The Amazon Connect team processes your request and assists you with the number porting process\. 

Porting phone numbers typically takes between two to four weeks after you submit the required information\. The amount of time depends on the complexity of the request and your current carrier\. Porting toll\-free numbers, or requests to port a large quantity of numbers at one time, usually take longer than porting local, direct dial numbers\.

We recommend that you select a phone number for Amazon Connect so that you can become familiar with the service while waiting for your number to be ported\.

**To port your current phone number to Amazon Connect**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Log in with the account used to create the Amazon Connect instance to which to port your current number\.

1. Choose **Support**, **Support Center**\.

1. On the **Support Center** page, choose **Create Case**\.

1. Fill in values for the following fields:
   + For **Regarding**, choose **Service Limit Increase**\.
   + For **Limit Type**, choose **Connect**\.
   + For **Region**, select the Region in which you created your Amazon Connect instance\.
   + For **Limit**, choose **Phone Number Porting**\.
   + For **New limit value**, enter the number of phone numbers to port\.
   + For **Use Case Description**, include as much information as possible about your request, including whether the numbers are Direct Inward Dial or toll\-free, your current carrier, and the contact information for the person authorized to make changes to your current phone service\. If you do not know all of these details, you may leave information out\.

1. Fill in the rest of the form, and choose **Submit**\.

### About Porting Phone Numbers<a name="about-porting"></a>

When you port your current phone number into Amazon Connect, we provide any possible assistance\. However, many of the steps are performed by telecommunications carriers\. 

We collect the information necessary to verify that you are authorized to port the numbers that you request\. We pass that information on to your existing carrier, and coordinate with the new carrier to get your number ported\. Each carrier has their own process and requirements for number porting\. Your number cannot be ported until your current carrier verifies that you own and are authorized to port the numbers requested\. Your current carrier must approve the request to port your number before the new carrier can provision the number\. After that is complete, the Amazon Connect team can start configuring your Amazon Connect instance to use the ported numbers\.

The steps in the porting process are as follows:

1. Submit a support ticket to port your number\.

1. Confirm number portability\. The Amazon Connect team confirms whether the numbers that you request can be ported from your current carrier\. We then contact you with next steps, or notify you that the requested numbers cannot be ported\.

1. Complete the Letter of Authorization/Agency \(LOA\)\. When you complete the LOA form, the information you provide must match the information on file with your current carrier\. If the information does not match, it may delay the porting of your number\. The LOA form authorizes your current carrier to release your number and allow it to be ported\. If your number can be ported, we provide you with an LOA form appropriate for the type of number to port\. There are different forms for local, Direct Inward Dial \(DID\), and toll\-free numbers\. If you are porting multiple numbers from different carriers, fill out a separate form for each carrier\.

   On the LOA form, include the following: 
   + The numbers to port
   + Information about your current carrier, such as a phone bill
   + Contact information for the person authorized to make changes to your phone service

1. To get the port started, the Amazon Connect team submits the LOA to the carrier for Amazon Connect on your behalf\. The new carrier works with your current carrier to move your current number over to their service\. This step typically takes 3–5 business days\.

   If your current carrier is able to validate and approve your request, they provide a date for the number to be ported to Amazon Connect\.

   If your current carrier rejects the request to port your number due to the LOA not having correct or complete information, the Amazon Connect team contacts you and requests a new LOA to submit to the carrier\.

When we receive a date from your current carrier, we start adding the numbers to your Amazon Connect instance about a day before the scheduled date\.

## Integrate with Your CRM<a name="setupintegration"></a>

You can integrate Amazon Connect with the Salesforce and Zendesk CRMs\. Integration allows you to launch your contact center in your CRM of choice, maintain your existing user base, and use the Amazon Connect cloud\-based infrastructure\.

To integrate the Contact Control Panel \(CCP\) into your CRM, see [Amazon Connect Contact Streams](https://github.com/aws/amazon-connect-streams)\. When completed, add the origin URLs to your instance settings\. This enables communication between Amazon Connect and your CRM\. For more information, see [Application Integration](amazon-connect-instance.md#app-integration)\.

## Remove Your Amazon Connect Instance<a name="delete-instance"></a>

If you no longer want to use an Amazon Connect instance, you can delete it\. If you delete an instance, the phone number claimed for the instance is released\. You lose all settings, data, metrics, and reports associated with the instance\.

**Important**  
You cannot undo the deletion of an instance or restore settings or data from the instance after it is deleted\.

**To delete an Amazon Connect instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Select the check box for the instance and choose **Remove**\.

1. When prompted, type the name of the instance and choose **Remove**\.