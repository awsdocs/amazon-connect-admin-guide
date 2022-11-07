# Configure SAML with IAM for Amazon Connect<a name="configure-saml"></a>

Amazon Connect supports identity federation by configuring Security Assertion Markup Language \(SAML\) 2\.0 with AWS IAM to enable web\-based single sign\-on \(SSO\) from your organization to your Amazon Connect instance\. This allows your users to sign in to a portal in your organization hosted by a SAML 2\.0 compatible identity provider \(IdP\) and log in to an Amazon Connect instance with a single sign\-on experience without having to provide separate credentials for Amazon Connect\.

## Important notes<a name="saml-important-notes"></a>

Before you begin, note the following:
+ Choosing SAML 2\.0\-based authentication as the identity management method for your Amazon Connect instance requires the configuration of [AWS Identity and Access Management federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_enable-console-saml.html)\. 
+ The user name in Amazon Connect must match the RoleSessionName SAML attribute specified in the SAML response returned by the identity provider\.
+ An Amazon Connect user can only be associated with a single AWS IAM Role\. Changing the AWS IAM Role used for federation will cause previously federated users to fail on login\. For more information about Identity and Access Management user and role management, see [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)\. 

## Overview of using SAML with Amazon Connect<a name="saml-overview"></a>

The following diagram shows the flow for SAML requests to authenticate users and federate with Amazon Connect\.

![\[Overview of the request flow for SAML authentication requests with Amazon Connect.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-overview.png)

SAML requests go through the following steps:

## 

1. The user browses to an internal portal that includes a link to log in to Amazon Connect\. The link is defined in the identity provider\.

1. The federation service requests authentication from the organization's identity store\.

1. The identity store authenticates the user and returns the authentication response to the federation service\.

1. When authentication is successful, the federation service posts the SAML assertion to the user's browser\.

1. The user's browser posts the SAML assertion to the AWS sign in SAML endpoint \(https://signin\.aws\.amazon\.com/saml\)\. AWS sign in receives the SAML request, processes the request, authenticates the user, and forwards the authentication token to Amazon Connect\.

1. Using the authentication token from AWS, Amazon Connect authorizes the user and opens Amazon Connect in their browser\.

## Enabling SAML\-based authentication for Amazon Connect<a name="enable-saml"></a>

The following steps are required to enable and configure SAML authentication for use with your Amazon Connect instance:

1. Create an Amazon Connect instance and select SAML 2\.0\-based authentication for identity management\.

1. Enable SAML federation between your identity provider and AWS\.

1. Add Amazon Connect users to your Amazon Connect instance\. Log in to your instance using the administrator account created when you created your instance\. Go to the **User Management** page and add users\. 
**Important**  
Due to the association of an Amazon Connect user and an AWS IAM Role, the user name must match exactly the RoleSessionName as configured with your AWS IAM federation integration, which typically ends up being the user name in your directory\. 

    The format should match the intersection of the format conditions of the [RoleSessionName](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) and an [Amazon Connect user](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateUser.html#connect-CreateUser-request-DirectoryUserId), as shown in the following diagram:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-ven-diagram.png)

   Format:
   + String: Upper\- and lower\-case alphanumeric characters with no spaces
   + Length constraints: Minimum length of 2\. Maximum length of 64\.
   + Special characters: **@** **\-** **\.** 

1. Configure your identity provider for the SAML assertions, authentication response, and relay state\. Users log in to your identity provider\. When successful, they are redirected to your Amazon Connect instance\. The IAM role is used to federate with AWS, which allows access to Amazon Connect\.

## Select SAML 2\.0\-based authentication during instance creation<a name="create-saml-instance"></a>

When you are creating your Amazon Connect instance, select the SAML 2\.0\-based authentication option for identity management\. On the second step, when you create the administrator for the instance, the user name that you specify must exactly match a user name in your existing network directory\. There is no option to specify a password for the administrator because passwords are managed through your existing directory\. The administrator is created in Amazon Connect and assigned the **Admin** security profile\.

You can log in to your Amazon Connect instance, through your IdP, using the administrator account to add additional users\.

## Enable SAML federation between your identity provider and AWS<a name="enable-saml-federation"></a>

To enable SAML\-based authentication for Amazon Connect, you must create an identity provider in the IAM console\. For more information, see [Enabling SAML 2\.0 Federated Users to Access the AWS Management Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_enable-console-saml.html)\.

The process to create an identity provider for AWS is the same for Amazon Connect\. Step 6 in the above flow diagram shows the client is sent to your Amazon Connect instance instead of the AWS Management Console\.

The steps necessary to enable SAML federation with AWS include:

1. Create a SAML provider in AWS\. For more information, see [Creating SAML Identity Providers](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_saml.html)\.

1. Create an IAM role for SAML 2\.0 federation with the AWS Management Console\. Create only one role for federation \(only one role is needed and used for federation\)\. The IAM role determines which permissions the users that log in through your identity provider have in AWS\. In this case, the permissions are for accessing Amazon Connect\. You can control the permissions to features of Amazon Connect by using security profiles in Amazon Connect\. For more information, see [Creating a Role for SAML 2\.0 Federation \(Console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_saml.html)\.
**Important**  
Replacing this Role causes previously federated users to fail at login because it breaks existing user logins due to the immutable Amazon Connectuser association with the previous Role\.

   In step 5, choose **Allow programmatic and AWS Management Console access**\. Create the trust policy described in the topic in the procedure *To prepare to create a role for SAML 2\.0 federation*\. Then create a policy to assign permissions to your Amazon Connect instance\. Permissions start on step 9 of the *To create a role for SAML\-based federation* procedure\.

**To create a policy for assigning permissions to the IAM role for SAML federation**

   1. On the **Attach permissions policy** page, choose **Create policy**\.

   1. On the **Create policy** page, choose **JSON**\.

   1. Copy one of the following example policies and paste it into the JSON policy editor, replacing any existing text\. You can use either policy to enable SAML federation, or customize them for your specific requirements\.

      Use this policy to enable federation for all users in a specific Amazon Connect instance\. For SAML\-based authentication, replace the value for the `Resource` to the ARN for the instance that you created:

      ```
      {
          "Version": "2012-10-17",
         "Statement": [
              {
                  "Sid": "Statement1",
                  "Effect": "Allow",
                  "Action": "connect:GetFederationToken",
                  "Resource": [
                      "arn:aws:connect:us-east-1:361814831152:instance/2fb42df9-78a2-2e74-d572-c8af67ed289b/user/${aws:userid}"
                  ]
              }
          ]
      }
      ```

      Use this policy to enable federation to a specific Amazon Connect instances\. Replace the value for the `connect:InstanceId` to the instance ID for your instance\.

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "Statement2",
                  "Effect": "Allow",
                  "Action": "connect:GetFederationToken",
                  "Resource": "*",
                  "Condition": {
                      "StringEquals": {
                          "connect:InstanceId": "2fb42df9-78a2-2e74-d572-c8af67ed289b"
                      }
                  }
              }
          ]
      }
      ```

      Use this policy to enable federation for multiple instances\. Note the brackets around the listed instance IDs\.

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "Statement2",
                  "Effect": "Allow",
                  "Action": "connect:GetFederationToken",
                  "Resource": "*",
                  "Condition": {
                      "StringEquals": {
                          "connect:InstanceId": [
                          "2fb42df9-78a2-2e74-d572-c8af67ed289b", 
                          "1234567-78a2-2e74-d572-c8af67ed289b"]
                      }
                  }
              }
          ]
      }
      ```

   1. After you create the policy, choose **Next: Review**\. Then return to step 10 in the *To create a role for SAML\-based federation* procedure in the [Creating a Role for SAML 2\.0 Federation \(Console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_saml.html) topic\.

1. Configure your network as a SAML provider for AWS\. For more information, see [Enabling SAML 2\.0 Federated Users to Access the AWS Management Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_enable-console-saml.html)\.

1. Configure SAML Assertions for the Authentication Response\. For more information, [Configuring SAML Assertions for the Authentication Response](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_saml_assertions.html)\.

1. For Amazon Connect, leave the **Application Start URL** blank\.

1. Configure the relay state of your identity provider to point to your Amazon Connect instance\. The URL to use for the relay state is comprised as follows:

   `https://region-id.console.aws.amazon.com/connect/federate/instance-id`

   Replace the *region\-id* with the Region name where you created your Amazon Connect instance, such as us\-east\-1 for US East \(N\. Virginia\)\. Replace the *instance\-id* with the instance ID for your instance\.

   For a GovCloud instance, the URL is **https://console\.amazonaws\-us\-gov\.com/**:  
   + https://console\.amazonaws\-us\-gov\.com/connect/federate/instance\-id
**Note**  
You can find the instance ID for your instance by choosing the instance alias in the Amazon Connect console\. The instance ID is the set of numbers and letters after '/instance' in the **Instance ARN** displayed on the **Overview** page\. For example, the instance ID in the following Instance ARN is *178c75e4\-b3de\-4839\-a6aa\-e321ab3f3770*\.  
arn:aws:connect:us\-east\-1:450725743157:instance/*178c75e4\-b3de\-4839\-a6aa\-e321ab3f3770*

## Configurations for regionally isolated SAML sign in<a name="regionally-isolated-saml"></a>

Perform the following steps to use regional SAML endpoints\. These steps are IdP agnostic; they work for any SAML IdP \(for example, Okta, Ping, OneLogin, Shibboleth, ADFS, AzureAD, and more\)\.

1. Update \(or override\) the AssertionConsumerService\. There are two ways you can do this:
   + **Option 1**: Download the AWS SAML metadata and update the `Location` attribute to the Region of your choice\. Load this new version of the AWS SAML metadata into your IdP\. 

     Following is an example of a revision:

      `<AssertionConsumerService index="1" isDefault="true" Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://region-id.signin.aws.amazon.com/saml"/>`
   + **Option 2**: Override the AssertionConsumerService \(ACS\) URL in your IdP\. For IdPs like Okta that provide prebaked AWS integrations, you can override the ACS URL in the AWS admin console\. Use the same format to override to a Region of your choice \(for example, https://*region\-id*\.signin\.aws\.amazon\.com/saml\)\.

1. Update the associated role trust policy:

   1. This step needs to be done for every role in every account that trusts the given identity provider\.

   1. Edit the trust relationship, and replace the singular `SAML:aud` condition with a multivalued condition\. For example:
      + Default: "`SAML:aud`": "https://signin\.aws\.amazon\.com/saml"\. 
      + With modifications: "`SAML:aud`": \[ "https://signin\.aws\.amazon\.com/saml", "https://*region\-id*\.signin\.aws\.amazon\.com/saml" \]

   1. Make these changes to the trust relationships in advance\. They should not be done as part of a plan during an incident\.

1. Configure a relay state for the Region\-specific console page\.

   1. If you don't do this final step, there's no guarantee that the Region\-specific SAML sign in process will forward the user to the console sign in page within the same Region\. This step is most varied per identity provider, but there are a blogs \(for example, [How to Use SAML to Automatically Direct Federated Users to a Specific AWS Management Console Page](http://aws.amazon.com/blogs/security/how-to-use-saml-to-automatically-direct-federated-users-to-a-specific-aws-management-console-page/)\) that show the use of relay state to achieve deep linking\.

   1. Using the technique/parameters appropriate for your IdP, set the relay state to the console endpoint that matches \(for example, https://*region\-id*\.console\.aws\.amazon\.com/connect/federate/*instance\-id*\)\.

**Note**  
Ensure that STS is not disabled in your additional Regions\.
Ensure no SCPs are preventing STS actions in your additional Regions\.

## Use a destination in your relay state URL<a name="destination-relay"></a>

When you configure the relay state for your identity provider, you can use the destination argument in the URL to navigate users to a specific page in your Amazon Connect instance\. For example, use a link to open the CCP directly when an agent logs in\. The user must be assigned a security profile that grants access to that page in the instance\. For example, to send agents to the CCP, use a URL similar to the following for the relay state\. You must use [URL encoding](https://en.wikipedia.org/wiki/Percent-encoding) for the destination value used in the URL:
+ `https://us-east-1.console.aws.amazon.com/connect/federate/instance-id?destination=%2Fconnect%2Fccp-v2`

For a GovCloud instance, the URL is **https://console\.amazonaws\-us\-gov\.com/**\. So the address would be: 
+ https://console\.amazonaws\-us\-gov\.com/connect/federate/instance\-id?destination=%2Fconnect%2Fccp\-v2

## Add users to your Amazon Connect instance<a name="saml-add-users"></a>

Add users to your connect instance, making sure that the user names exactly match the users names in your existing directory\. If the names do not match, users can log in to the identity provider, but not to Amazon Connect because no user account with that user name exists in Amazon Connect\. You can add users manually on the **User management** page, or you can bulk upload users with the CSV template\. After you add the users to Amazon Connect, you can assign security profiles and other user settings\.

When a user logs in to the identity provider, but no account with the same user name is found in Amazon Connect, the following **Access denied** message is displayed\.

![\[Error message displayed when a user tries to log in to Amazon Connect through their identity provider when the user name is not in Amazon Connect.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-access-denied.png)
<a name="bulk-user-upload"></a>
**Bulk upload users with the template**  
You can import your users by adding them to a CSV file\. You can then import the CSV file to your instance, which adds all users in the file\. If you add users by uploading a CSV file, make sure that you use the template for SAML users\. You can find on the **User management** page in Amazon Connect\. A different template is used for SAML\-based authentication\. If you previously downloaded the template, you should download the version available on the **User management** page after you set up your instance with SAML\-based authentication\. The template should not include a column for email or password\.

## SAML user logging in and session duration<a name="user-sessions"></a>

When you use SAML in Amazon Connect, users must log in to Amazon Connect through your identity provider \(IdP\)\. Your IdP is configured to integrate with AWS\. After authentication, a token for their session is created\. The user is then redirected to your Amazon Connect instance and automatically logged in to Amazon Connect using single sign\-on\.

As a best practice, you should also define a process for your Amazon Connect users to log out when they are finished using Amazon Connect\. They should log out from both Amazon Connect and your identity provider\. If they do not, the next person that logs in to the same computer can log in to Amazon Connect without a password since the token for the previous sessions is still valid for the duration of the session\. It's valid for 10 hours\.
<a name="session-expire"></a>
**About session expiration**  
Amazon Connect sessions expire 10 hours after a user logs in\. After 10 hours, users are automatically logged out, even if they are currently on a call\. If your agents stay logged in for more than 10 hours, they need to refresh the session token before it expires\. To create a new session, agents need to log out of Amazon Connect and your IdP and then log in again\. This resets the session timer set on the token so that agents are not logged out during an active contact with a customer\. When a session expires while a user is logged in, the following message is displayed\. To use Amazon Connect again, the user needs to log in to your identity provider\.

![\[Error message displayed when the session expires for a SAML-based user.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-session-expired.png)