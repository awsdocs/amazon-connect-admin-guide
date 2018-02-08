# Getting Started with Amazon Connect<a name="gettingstarted"></a>

An Amazon Connect instance is the starting point for your contact center\. When your instance has launched, you can edit the resource configuration settings, which include data storage, integration with CRM systems, and analytics\. Then, you can launch your instance from the AWS Management Console, follow the onboarding steps, and begin using your contact center\.

Part of this tutorial refers to the Amazon Connect Contact Control Panel \(CCP\)\. The CCP is built in to the Amazon Connect Contact Center Manager \(CCM\)\. After you have claimed and tested your number, you can start using the CCP immediately\. For more information, see [Using the Contact Control Panel](http://docs.aws.amazon.com/connect/latest/userguide/agentconsole.html) in the *Amazon Connect User Guide*\.

To get started with using Amazon Connect, you first create an instance, which is the basis of your contact center\. You can edit your instance's resource settings in the AWS Management Console\. After your instance has been created, it is accessible through a unique URL, which is used by agents, administrators, and managers to open the CCM and access the CCP\. For more information, see [How Amazon Connect Works](what-is-amazon-connect.md#amazon-connect-fundamentals)\.

## Before You Begin<a name="prerequisites"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Amazon Connect\. You are charged only for the services that you use\.

If you have an AWS account already, skip to the next task\. If you don't have an AWS account, use the following procedure to create one\.

**To create an AWS account**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.
**Note**  
This might be unavailable in your browser if you previously signed into the AWS Management Console\. In that case, choose **Sign in to a different account**, and then choose **Create a new AWS account**\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a PIN using the phone keypad\.

## Create an Amazon Connect Instance<a name="launch-contact-center"></a>

You can create or add an instance as follows\. These steps are intended to help you get started quickly; some advanced settings are not be included\.

**To create an Amazon Connect instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose **Add an instance**\.

1. For the **Identity management** step, choose **Store users within Amazon Connect** and type a domain name to complete **Access URL**\. This domain is used in your contact center URL and cannot be changed\. The alias must be globally unique, meaning that an alias can be used only once across all Amazon Connect instances and regions\. Choose **Next step**\.

1. For the **Administrator** step, you can choose to add an administrator from your directory, create a new administrator, or skip this step for now and add an administrator later on\.

1. For the **Telephony options** step, indicate whether you'd like your contact center to accept calls, make calls, or both\. You can set the user permissions within the Amazon Connect web application\. The telephone number options are provided after setup\.

1. For the **Data storage** step, you can keep the default settings or choose **Advanced settings** in order to customize settings\. For more information, see [Data Storage](amazon-connect-instance.md#datastorage)\.

1. For the **Review and create** step, review your settings and then choose **Create instance**\.
**Important**  
This is the only time you can change the directory and domain name settings—you can edit any other setting later on\.

1. After your instance is created, choose **Get started** to select and test a phone number\. Amazon Connect automatically configures your instance to use the phone number that you select\.
**Note**  
For information about how to use your current phone number with Amazon Connect, see [Port Your Current Phone Number](#numberporting)\.

1. Provide your users with their user names and passwords so that they can log in and begin accepting and making calls\. For more information, see the [Amazon Connect User Guide](http://docs.aws.amazon.com/connect/latest/userguide/)\.

1. \(Optional\) Continue to configure your instance\. For more information, see [Configuring Your Amazon Connect Instance](amazon-connect-instance.md)\.

## Port Your Current Phone Number<a name="numberporting"></a>

To continue to use your current United States phone number with Amazon Connect, you can submit a support ticket to port the number to Amazon Connect\. The Amazon Connect team processes your request and assists you with the number porting process\. 

Porting phone numbers typically takes between two to four weeks after you submit the required information\. The amount of time depends on the complexity of the request and your current carrier\. Porting toll\-free numbers, or requests to port a large quantity of numbers at one time, usually take longer than porting local, direct dial numbers\.

We recommend that you select a phone number for Amazon Connect so that you can become familiar with the service while waiting for your number to be ported\.

**To port your current phone number to Amazon Connect**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Log in with the account used to create the Amazon Connect instance to which to port your current number, and choose **Support**, **Support Center**\.

1. On the **Support Center** page, choose **Create Case**\.

1. For **Regarding**, select **Service Limit Increase**\.

1. For **Limit Type**, select **Connect**\.

1. For **Region**, select the region in which you created your Amazon Connect instance\.

1. For **Limit**, select **Phone Number Porting**\.

1. For **New limit value**, enter the number of phone numbers to port\.

1. For **Use Case Description**, include as much information as possible about your request, including whether the numbers are Direct Inward Dial or toll\-free, your current carrier, and the contact information for the person authorized to make changes to your current phone service\. If you do not know all of these details, you may leave information out\.

1. Fill in the rest of the form, and choose **Submit**\.

### About Porting Phone Numbers<a name="about-porting"></a>

When you port your current phone number into Amazon Connect, we provide any possible assistance\. However, many of the steps are performed by telecommunications carriers\. 

We collect the information necessary to verify that you are authorized to port the numbers that you request\. We pass that information on to your existing carrier, and coordinate with the new carrier to get your number ported\. Each carrier has their own process and requirements for number porting\. Your number cannot be ported until your current carrier verifies that you own and are authorized to port the numbers requested\. Your current carrier must approve the request to port your number before the new carrier can provision the number\. After that is complete, the Amazon Connect team can start configuring your Amazon Connect instance to use the ported numbers\.

The steps in the porting process are as follows:

1. Submit a support ticket to port your number\.

1. Confirm number portability\. The Amazon Connect team confirms whether the numbers that you request can be ported from your current carrier\. We then contact you with next steps, or notify you that the requested numbers cannot be ported\.

1. Complete the Letter of Authorization/Agency \(LOA\)\. When you complete the LOA form, the information you provide must match the information on file with your current carrier\. If the information does not match, it may delay the porting of your number\. The LOA form authorizes your current carrier to release your number and allow it to be ported\. If your number can be ported, we provide you with an LOA form appropriate for the type of number to port\. There are different forms for local, Direct Inward Dial \(DID\), and toll\-free numbers\. If you are porting multiple numbers from different carriers, fill out a separate form for each carrier\.

   On the LOA form, include the numbers to port; information about your current carrier, such as a phone bill; and contact information for the person authorized to make changes to your phone service\.

1. To get the port started, the Amazon Connect team submits the LOA to the carrier for Amazon Connect on your behalf\. The new carrier works with your current carrier to move your current number over to their service\. This step typically takes 3–5 business days\.

   If your current carrier is able to validate and approve your request, they provide a date for the number to be ported to Amazon Connect\.

   If your current carrier rejects the request to port your number due to the LOA not having correct or complete information, the Amazon Connect team contacts you and requests a new LOA to submit to the carrier\.

When we receive a date from your current carrier, we start adding the numbers to your Amazon Connect instance about a day before the scheduled date\.

## Integrate with Your CRM<a name="setupintegration"></a>

You can integrate Amazon Connect with the Salesforce and Zendesk CRMs\. Integration allows you to launch your contact center in your CRM of choice, maintain your existing user base, and use the Amazon Connect cloud\-based infrastructure\.

To integrate the Contact Control Panel \(CCP\) into your CRM, see [Amazon Connect Contact Streams](https://github.com/aws/amazon-connect-streams)\. When completed, add the origin URLs to your instance settings\. This enables communication between Amazon Connect and your CRM\. For more information, see [Application Integration](amazon-connect-instance.md#app-integration)\.

## Delete Your Amazon Connect Instance<a name="delete-instance"></a>

If you no longer wish to use an Amazon Connect instance, you can delete it\. Any directories, buckets, or administrators that are associated with the instance are also deleted\.

**Important**  
This operation cannot be canceled or undone\.

**To delete an Amazon Connect instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Select the check box for the instance and choose **Remove**\.

1. When prompted, type the name of the instance and choose **Remove**\.