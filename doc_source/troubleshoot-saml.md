# Troubleshoot SAML with Amazon Connect<a name="troubleshoot-saml"></a>

This article explains how to troubleshoot and resolve some of the most common issues customers encounter when using SAML with Amazon Connect\.

## Error Message: Access Denied\. Your account has been authenticated, but has not been onboarded to this application\.<a name="troubleshoot-saml-access-denied"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-access-denied.png)

### What does this mean?<a name="troubleshoot-saml-access-denied-what"></a>

This error means that the user has successfully authenticated via SAML into the AWS SAML login endpoint\. However, the user could not be matched/found inside Amazon Connect\. This usually indicates one of the following: 
+ The username in Amazon Connect doesn't match the `RoleSessionName` SAML attribute specified in the SAML response returned by the identity provider\.
+ The user doesn't exist in Amazon Connect\.
+ The user have two separate profiles assigned to them with SSO\.

### Resolution<a name="troubleshoot-saml-access-denied-resolution"></a>

Use the following steps to check the RoleSessionName SAML attribute specified in the SAML response returned by the identity provider, and then retrieve and compare with the login name in Amazon Connect\. 

1. Perform a HAR capture \(**H**TTP **AR**chive\) for the end\-to\-end login process\. This captures the network requests from the browser side\. Save the HAR file with your preferred file name, for example, **saml\.har**\. 

   For instructions, see [How do I create a HAR file from my browser for an AWS Support case?](https://aws.amazon.com/premiumsupport/knowledge-center/support-case-browser-har-file/) 

1. Use a text editor to find the SAMLResponse in the HAR file\. Or, run the following commands:

   `$ grep -o "SAMLResponse=.*&" azuresaml.har | sed -E 's/SAMLResponse=(.*)&/\1/' > samlresponse.txt`
   + This searches for the SAMLresponse in the HAR file and saves it to a **samlresponse\.txt** file\.
   + The response is URL encoded and the contents are Base64 encoded\.

1. Decode the URL response and then decode the Base64 contents using a third\-party tool or a simple script\. For example:

   `$ cat samlresponse.txt | python3 -c "import sys; from urllib.parse import unquote; print(unquote(sys.stdin.read()));" | base64 --decode > samlresponsedecoded.txt`

   This script uses a simple python command to decode the SAMLResponse from its original URL encoded format\. Then it decodes the response from Base64 and outputs the SAML Response in plain text format\.

1. Check the decoded response for the needed attribute\. For example, the following image shows how to check `RoleSessionName`:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-rolesessionname.png)

1. Check whether the username returned in from the previous step exists as a user in your Amazon Connect instance:

   $ aws connect list\-users \-\-instance\-id \[INSTANCE\_ID\] \| grep $username
   + If the final grep does not return a result then this means that the user does not exist in your Amazon Connect instance or it has been created with a different case/capitalization\.
   + If your Amazon Connect instance has many users, the response from the ListUsers API call maybe paginated\. Use the `NextToken` returned by the API to fetch the rest of the users\. For more information, see [ListUsers](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListUsers.html)\.

### Example SAML Response<a name="example-samlresponse"></a>

Following is an image from a sample SAML Response\. In this case, the identity provider \(IdP\) is Azure Active Directory \(Azure AD\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-saml-response.png)

## Error Message: Bad Request\. The request was not valid and could not be processed\.<a name="troubleshoot-saml-bad-request"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-bad-request.png)

### What does this mean?<a name="troubleshoot-saml-bad-request-what"></a>

One of the most common reasons for this error is an Amazon Connect user logged in previously using a different identity provider\. For example, first they logged in using this attribute name: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-old-attribute-name-login.png)

Then the same user tried to login but with a different `Role` SAML Attribute, for example: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-new-attribute-name-login.png)

### Resolution<a name="troubleshoot-saml-bad-request-resolution"></a>

The recommended solution is to reuse the existing Role associated with the Amazon Connect user and [edit the trust relationship](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-editing-console.html#roles-managingrole_edit-trust-policy) to reference a new identity provider or service principal to meet your new authentication requirements\. If you do need to associate an Amazon Connect user with a new Role, you need to delete and recreate the user in the existing Amazon Connect instance which will result in the loss of data for that user\. 

 For instructions for doing this in the Amazon Connect console, see [Manage users in Amazon Connect](manage-users.md)\. Or, use these commands for doing this from the AWS CLI:

1. Get the user ID:

   `aws connect list-users --instance-id [INSTANCE_ID]`

1. Delete the user account:

   `aws connect delete-user --instance-id [INSTANCE_ID] --user-id [USER_ID]` 

1. Create the user account:

   `aws create-user --username [USER_ID] --phone-config [PHONE_CONFIG] --security-profile-ids [SECURITY_PROFILE_ID] --routing-profile-id [ROUTING_PROFILE_ID] --instance-id [INSTANCE_ID]` 

You can also complete these actions using the [AWS SDKs](http://aws.amazon.com/tools/)\. 

## Error Message: Access denied, Please contact your AWS account administrator for assistance\.<a name="troubleshoot-saml-contact-admin"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/saml-troubleshooting-access-denied-admin.png)

### What does this mean?<a name="troubleshoot-saml-bad-request-what"></a>

The role that the user has assumed has successfully authenticated via SAML\. However, the role doesn't have permission to call the GetFederationToken API for Amazon Connect\. This call is required so the user can log in to your Amazon Connect instance using SAML\.

### Resolution<a name="troubleshoot-saml-bad-request-resolution"></a>

1. Attach a policy that has the permissions for `connect:GetFederationToken` to the role found in the error message\. Following is a sample policy:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [{
           "Sid": "Statement1",
           "Effect": "Allow",
           "Action": "connect:GetFederationToken",
               "Resource": [
               "arn:aws:connect:ap-southeast-2:xxxxxxxxxxxx:instance/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/user/${aws:userid}"
               ]
           }
       ]
   }
   ```

1. Use the IAM console to attach the policy\. Or, use the attach\-role\-policy API, for example:

   `$ aws iam attach-role-policy —role-name [ASSUMED_ROLE] —policy_arn [POLICY_WITH_GETFEDERATIONTOKEN]`
