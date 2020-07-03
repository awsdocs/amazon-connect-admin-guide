# Configure SAML with an AWS SSO application for Amazon Connect<a name="configure-saml-with-aws-sso"></a>

AWS SSO provides support for integration with other services through built\-in applications\. These applications use AWS SSO for authentication and provide end\-users with an easy sign\-in experience\. To learn more about AWS SSO applications, see [What is AWS Single Sign\-On?](https://docs.aws.amazon.com/singlesignon/latest/userguide/) in the *AWS SSO User Guide*\.

When you set up an Amazon Connect AWS SSO\-integrated application, your users are able to sign\-in to AWS SSO, click on the application icon, and seamlessly authenticate via SAML into your Amazon Connect instance with minimal extra setup\.

## Prerequisites<a name="configure-saml-with-aws-sso-prerequisites"></a>
+ Set up AWS SSO\. For instructions, see [Getting Started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the [AWS Single Sign\-On User Guide](https://docs.aws.amazon.com/singlesignon/latest/userguide/)\.
+ Set up your Amazon Connect instance for SAML federation\. For instructions and important notes, see [Configure SAML with IAM for Amazon Connect](configure-saml.md)\. 

## Overview of SAML federation with AWS SSO\-integrated application<a name="configure-saml-with-aws-sso-overview"></a>

Depending on your AWS SSO IdP configuration, the flow between AWS SSO and your IdP will vary\. The following diagram shows the basic SAML authentication flow from an initial AWS SSO sign\-on through authentication into your Amazon Connect instance\.

![\[Overview of the request flow for SAML authentication requests with Amazon Connect.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-sso-overview.png)

SAML requests go through the following steps:

## 

1. The user browses to an AWS SSO user portal\. They are redirected to your identity provider's \(IdP\) sign\-on page \(for external IdPs\) with a SAML request\.

1. The IdP authenticates the user’s credentials and their multi\-factor authentication \(MFA\) as configured\.

1. After the user is authenticated, the IdP sends the SAML response to AWS SSO\.

1. AWS SSO displays the user’s assigned accounts, roles, and applications on the landing page\.

1. The user selects Amazon Connect from the list of accounts and applications\.

1. The application redirects the user with AWS IAM SAML assertion for authorization into the AWS console\.

1. The user is automatically redirected to the Amazon Connect instance based on the application’s relay state\.

## Step 1: Configure your Amazon Connect AWS SSO application<a name="how-to-configure-saml-with-aws-sso"></a>

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/console) \(https://console\.aws\.amazon\.com/console\) using your AWS account\. 

1. Go to AWS Single Sign\-On\. If needed, choose **Enable SSO**\. 

1. In the AWS SSO console, in the left navigation menu, choose **Applications**\. Then choose **Add a new application**\.

1. On the **Add New Application** page, type **Amazon Connect** and choose it\. Then choose **Add application**\.

1. On the **Configure Amazon Connect** page, under **Details**, enter a display name for the application\. We suggest that you choose a unique display name if you plan to have more than one instance of Amazon Connect\.

1. Under **AWS SSO metadata**, do the following:

   1. Next to **AWS SSO SAML metadatafile**, choose **Download**, **Save file** to download and save the identity provider metadata\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sso-metadata.png)

   1. Next to **AWS SSO certificate**, choose **Download certificate**, **Save File** to download and save the identity provider certificate\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sso-certificate.png)

      You will need these files later when you do [Step 2: Configure your IAM resources](#how-to-configure-your-iam-resources)\.

1. Under **Application properties**, set the **Relay State** and **Session Duration** for your Amazon Connect instance:

   1. The URL to use for the relay state is:

      `https://region-id.console.aws.amazon.com/connect/federate/instance-id`

      For example, `https://us-west-2.console.aws.amazon.com/connect/federate/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee`

      You can locate your region ID on the upper righter corner of the console\. To find your Amazon Connect instance id, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.

   1. The default session duration for an Amazon Connect instance is 10 hours\. We recommend you set the session duration to match or exceed your instance’s duration\. For more information, see [SAML user logging in and session duration](configure-saml.md#user-sessions)\.

1. Under **Application metadata**, leave the default values\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sso-application-metadata.png)

1. Choose **Save changes**\.

## Step 2: Configure your IAM resources<a name="how-to-configure-your-iam-resources"></a>

1. Follow the steps in [Creating and Managing an IAM Identity Provider \(Console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_saml.html#idp-manage-identityprovider-console.html)\. In this step, you will upload the AWS SSO SAML metadata file that you created in [Step 1: Configure your Amazon Connect AWS SSO application](#how-to-configure-saml-with-aws-sso)\.

1. Follow the steps in [Creating a Role for SAML 2\.0 Federation \(Console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_saml.html) to create a role that establishes a trust relationship between IAM and the AWS SSO Amazon Connect SAML Provider created in the previous step\.
   + Choose **Allow programmatic and AWS Management Console access**\.

1. Embed an Inline Policy for the IAM Role that grants federated users access to your Amazon Connect instance\.

   Use this policy to enable federation to a specific Amazon Connect instances\. Replace the value for the `connect:InstanceId` to the instance ID for your instance\. For example:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "Statement1",
               "Effect": "Allow",
               "Action": "connect:GetFederationToken",
               "Resource": "*",
               "Condition": {
                   "StringEquals": {
                       "connect:InstanceID": "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeeee"
                   }
               }
           }     
       ]
   }
   ```

1. Go back to the AWS SSO console page where you are configuring Amazon Connect\.

1. Choose the **Attribute Mappings** tab and choose **Add new attribute mapping**\. Add an attribute for the role, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-sso.png)

1. Assign a user to the application in AWS SSO\. For instructions, see [Assign User Access](https://docs.aws.amazon.com/singlesignon/latest/userguide/assignuserstoapp.html) in the *AWS SSO User Guide*\.

1. Create a user in your Amazon Connect instance with the same user name \(email\) as your AWS SSO user\.
**Note**  
After a user name \(email\) is mapped to an IAM role on an Amazon Connect instance, that user cannot login via another SAML role \(for instance a separate SSO application or another IdP’s role\)\. To change a user’s role\-mapping, you must delete and re\-provision user on that instance\.

## Step 3: Verify access<a name="verifying-sso-from-aws-sso"></a>

1. Access the AWS SSO user portal using the credentials of a user assigned to Amazon Connect\.

1. In the list of applications, choose Amazon Connect to initiate a login to your Amazon Connect instance\.

1. If login was successful you will be signed\-in to the Amazon Connect instance\.

## User provisioning types<a name="user-provisioning-types"></a>

There are two user provisioning types you need to be aware of:
+ **Pre\-provisioned users**: These users must already exist in the downstream SaaS application\. For example, you may need to create SaaS users with the same subject as the AD users\.
+ **JIT users \(Just\-In\-Time\)**: These users do not necessarily exist in the downstream SaaS application, They are provisioned/created/registered the first time the user federates\. You may need to enable the JIT option in your SaaS application for the AD domain\.

Amazon Connect implements pre\-provisioned users when SAML authentication is used\. You need to add the users to the Amazon Connect instance before they try to sign\-on\. AWS SSO provisioning depends on the IdP you're using: 
+ If SSO or an external provider is your IdP, the pre\-provisioned users \(or manual entry\) model is used\.
+ If AD is your IdP, SSO JIT provisioning is used\.

The system for cross\-domain identity management \(SCIM\) provisioning protocol is another option for supported external IdPs\. For more information, see [Manage Identities in AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-sso.html)\.

## Troubleshoot SSO configuration<a name="troubleshooting-sso-configuration"></a>

The following table lists a couple of tips for troubleshooting your SSO configuration\. For more information, see [Troubleshooting AWS SSO Issues](https://docs.aws.amazon.com/singlesignon/latest/userguide/troubleshooting.html)\.


| Error | Issue | Solution | 
| --- | --- | --- | 
|  An error occurred when we tried to process your request\.  |  The **Application ACS URL** specified in the identity provider is incorrect\.  |  Make sure that the ACS URL in the AWS SSO application matches https://signin\.aws\.amazon\.com/saml\.  | 
|  Other  |  When AWS SSO creates a SAML Assertion for a user, it uses the value of the "email" field \(if they are present\) from the connected directory to populate the **Email** in the SAML assertion\. Many service providers expect these attributes to contain the user's email address\. By default, your directory is configured to send **windowsUPN** in both fields\.  |  Your directory may be configure to contain the user's email in the **Email** attribute instead\. If so, you may need to change this in your **Connected directory** settings\.   | 