# Security Best Practices for Amazon Connect<a name="security-best-practices"></a>

Amazon Connect provides a number of security features to consider as you develop and implement your own security policies\. The following best practices are general guidelines and don’t represent a complete security solution\. Because these best practices might not be appropriate or sufficient for your environment, treat them as helpful considerations rather than prescriptions\.

**Topics**
+ [Amazon Connect Preventative Security Best Practices](#bp-security-profiles)
+ [Amazon Connect Detective Security Best Practices](#bp-security-detective)

## Amazon Connect Preventative Security Best Practices<a name="bp-security-profiles"></a>
+ Ensure that all profile permissions are as restrictive as possible\. Allow access to only those resources absolutely required for the user's role\. For example, don't give agents permissions to create, read, or update users in Amazon Connect\.
+ Ensure that multi\-factor authentication \(MFA\) is set up through your SAML 2\.0 identity provider, or Radius server, if that's more applicable for your use case\. After MFA is set up, a third text box becomes visible on the Amazon Connect login page to provide the second factor\.
+ If you use an existing directory through AWS Directory Service or SAML\-based authentication for identity management, ensure that you follow all security requirements appropriate for your use case\. 
+ Use the **Log in for emergency access** URL on the instance page of the AWS console only in emergency situations, not for daily use\. For more information, see [Emergency admin login](emergency-admin-login.md)\.

### Use Service Control Policies \(SCPs\)<a name="use-scp"></a>

Service control policies \(SCPs\) are a type of organization policy that you can use to manage permissions in your organization\. An SCP defines a guardrail, or sets limits, on the actions that the account's administrator can delegate to users and roles in the affected accounts\. You can use SCPs to protect critical resources associated with your Amazon Connect workload\.

#### Set a Service Control Policy to prevent the deletion critical resources<a name="set-scp"></a>

If you’re using SAML 2\.0\-based authentication and delete the AWS IAM Role that is used for authenticating Amazon Connect users, users won't be able to login to the Amazon Connect instance\. You will need to delete and recreate users to be associated with a new Role\. This results in the deletion of all data associated with those users\. 

To prevent the accidental deletion of critical resources and to protect the availability of your Amazon Connect instance, you can set a [Service Control Policy](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) \(SCP\) as an additional control\. 

Following is an example SCP that can be applied at the AWS Account, Organizational Unit, or Organizational Root to prevent the deletion of the Amazon Connect instance and associated Role:

```
{    
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AmazonConnectRoleDenyDeletion",
      "Effect": "Deny",
      "Action": [
        "iam:DeleteRole"
      ],
      "Resource": [
        "arn:aws:iam::*:role/Amazon Connect user role"
      ]
    },
    {
      "Sid": "AmazonConnectInstanceDenyDeletion",
      "Effect": "Deny",
      "Action": [
        "connect:DeleteInstance"         
      ],
      "Resource": [
        "Amazon Connect instance ARN"
      ]
    }
  ]
}
```

## Amazon Connect Detective Security Best Practices<a name="bp-security-detective"></a>

Logging and monitoring are important for the availability, reliability and, performance of contact center\. You should log relevant information from Amazon Connect flows to CloudWatch and build alerts and notifications based on the same\.

Define log retention requirements and lifecycle policies early on, and plan to move log files to cost\-efficient storage locations as soon as practical\. Amazon Connect public APIs log to CloudTrail\. Review and automate actions based on CloudTrail logs\.

We recommend Amazon S3 for long\-term retention and archiving of log data, especially for organizations with compliance programs that require log data to be auditable in its native format\. Once log data is in an Amazon S3 bucket, define lifecycle rules to automatically enforce retention policies and move these objects to other, cost\-effective storage classes, such as Amazon S3 Standard \- Infrequent Access \(Standard \- IA\) or Amazon S3 Glacier\.

The AWS Cloud provides flexible infrastructure and tools to support both sophisticated partner offerings and self\-managed centralized\-logging solutions\. This includes solutions such as Amazon OpenSearch Service and Amazon CloudWatch Logs\.

You can implement fraud detection and prevention for incoming contacts by customizing Amazon Connect flows per your requirements\. For example, you can check incoming contacts against previous contact activity in Dynamo DB and then take actions such as disconnecting a contact who is on a deny list\. 