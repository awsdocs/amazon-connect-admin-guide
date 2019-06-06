# Amazon Connect Instances<a name="amazon-connect-instances"></a>

To create an Amazon Connect contact center, you create an virtual contact center instance\. Each instance contains all the resources and settings related to your contact center\. You can manage settings for your instance from the Amazon Connect console\. You can manage settings for your contact center from within your contact center instance\.

You can create multiple instances, but each instance functions only within the AWS Region in which you create it\. Settings, users, metrics, and reporting are not shared between instances\.

**Topics**
+ [Create an Instance](#create-connect-instance)
+ [Update Instance Settings](#update-instance-settings)
+ [Manage Users](#user-management)
+ [Enable Data Streaming](#data-streaming)
+ [Integrate with Your CRM](#setupintegration)
+ [Log in as Administrator](#log-in-as-admin)
+ [Delete Your Instance](#delete-connect-instance)

## Create an Instance<a name="create-connect-instance"></a>

To create a contact center instance, see [Get Started with Amazon Connect](amazon-connect-get-started.md)\.

## Update Instance Settings<a name="update-instance-settings"></a>

To update the instance settings, open the Amazon Connect console, choose the name of the instance from **Instance Alias**, and complete the following procedures\.

**To update the telephony options**

1. In the navigation pane, choose **Telephony**\.

1. \(Optional\) To enable customers to call into your contact center, choose **I want to handle incoming calls with Amazon Connect**\.

1. \(Optional\) To enable outbound calling from your contact center, choose **I want to make outbound calls with Amazon Connect**\.

1. Choose **Save**\.

**To update the data storage settings**

1. In the navigation pane, choose **Data storage**\.

1. \(Optional\) To specify the bucket and KMS key for call recordings, choose **Call recordings**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. \(Optional\) To enable live media streaming, choose **Live media streaming**, **Edit**\. For more information, see [Live Media Streaming in Contact Flows](customer-voice-streams.md)\.

1. \(Optional\) To specify the bucket and KMS key for exported reports, choose **Exported reports**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

**To enable data streaming**

1. In the navigation pane, choose **Data streaming**\.

1. Choose **Enable data streaming**\. For more information, see [Enable Data Streaming](#data-streaming)\.

1. For **Contact Trace Records**, do one of the following:
   + Choose **Kinesis Firehose** and select an existing delivery stream, or choose **Create a new Kinesis firehose** to open the Kinesis Firehose console and create the delivery stream\.
   + Choose **Kinesis Stream** and select an existing stream, or choose **Create a new Kinesis firehose** to open the Kinesis console and create the stream\.

1. For **Agent Events**, select an existing Kinesis stream or choose **Create a new Kinesis stream** to open the Kinesis console and create the stream\.

1. Choose **Save**\.

**To update the contact flow settings**

1. In the navigation pane, choose **Contact flows**\.

1. \(Optional\) To add a signing key for use in contact flows, choose **Add key**\. For more information, see [Add Security Keys](connect-contact-flows.md#contact-flow-keys)\.

1. \(Optional\) To integrate with Amazon Lex, select a Lex bot\. For more information, see [Add an Amazon Lex Bot](connect-contact-flows.md#amazon-lex)\.

1. \(Optional\) To integrate with AWS Lambda, select a Lambda function\. For more information, see [Lambda Functions in Contact Flows](connect-lambda-functions.md)\.

1. \(Optional\) To enable contact flow logs, choose **Enable contact flow logs**\. For more information, see [Contact Flow Logs](contact-flow-logs.md)\.

## Manage Users<a name="user-management"></a>

You can add users and configure them with permissions that are appropriate to their roles \(for example, agents or managers\)\. For more information, see [Amazon Connect Security Profiles](connect-security-profiles.md)\. Contacts can be routed based on the skills required of the agents\. For more information, see [Create a Routing Profile](connect-queues.md#routing-profiles)\.

**To add a user**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Choose **Create and set up a new user** and then choose **Next**\.

1. Enter the name, email address, and password for the user\.

1. Choose a routing profile and a security profile\.

1. Choose **Save**\.

**To update a user**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Users**, **User management**\.

1. Select the checkbox for one or more users and choose **Edit**\.

1. \(Optional\) To reset the password, choose **reset password**\. Specify a new password and then choose **Submit**\.

1. \(Optional\) Choose a routing profile\.

1. \(Optional\) Add or remove security profiles\.

1. \(Optional\) Update the agent hierarchy\.

1. Choose **Save**\.

## Enable Data Streaming<a name="data-streaming"></a>

You can export contact trace records \(CTRs\) and agent events from Amazon Connect and perform real\-time analysis on contacts\. Data streaming sends data to Amazon Kinesis\.

If you enable server\-side encryption for the Kinesis stream you select, Amazon Connect cannot publish to the stream because it does not have permission to call `kms:GenerateDataKey` so that it can encrypt data sent to Kinesis\. To work\-around this, enable encryption for call recordings or scheduled reports, create a customer master key \(CMK\) to use for encryption, and then choose the same CMK for the Kinesis data stream that you use for call recording or scheduled reports\. For more information, see [Creating Keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) in the *AWS Key Management Service Developer Guide*\.

## Integrate with Your CRM<a name="setupintegration"></a>

You can integrate Amazon Connect with the Salesforce and Zendesk CRMs\. Integration allows you to launch your contact center in your CRM of choice, maintain your existing user base, and use the Amazon Connect cloud\-based infrastructure\.

To integrate the Contact Control Panel \(CCP\) into your CRM, see [Amazon Connect Contact Streams](https://github.com/aws/amazon-connect-streams)\. When completed, add the origin URLs to your instance settings\. This enables communication between Amazon Connect and your CRM\. For more information, see [Application Integration](amazon-connect-contact-control-panel.md#app-integration)\.

## Log in as Administrator<a name="log-in-as-admin"></a>

A user assigned to the **Admin** security profile can log in to the instance with full administrator permissions from the Amazon Connect console\. This can be helpful if you forget the password for the administrator account\. Users assigned to other security profiles, such as **Agent**, don't have the permissions required to log in with administrator permissions\.

**To log in with administrator permissions**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the name of the instance from the **Instance Alias** column\.

1. In the navigation pane, choose **Overview**\.

1. Choose **Log in as administrator**\.

1. When prompted, enter your password and choose **Sign In**\.

**To log out**  
To log out of your instance, go to the title bar at the top of the screen and select the icon with the arrow \(**Log out**\) that appears next to your user name\.

## Delete Your Instance<a name="delete-connect-instance"></a>

If you no longer want to use an instance, you can delete it\. When you delete an instance, the phone number claimed for the instance is released\. You lose all settings, data, metrics, and reports associated with the instance\.

**Important**  
You cannot undo the deletion of an instance or restore settings or data from the instance after it is deleted\.

**To delete an instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Select the check box for the instance and choose **Remove**\.

1. When prompted, type the name of the instance and choose **Remove**\.