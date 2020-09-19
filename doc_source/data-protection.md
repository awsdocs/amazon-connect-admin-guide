# Data protection in Amazon Connect<a name="data-protection"></a>

Amazon Connect conforms to the AWS [shared responsibility model](http://aws.amazon.com/compliance/shared-responsibility-model/), which includes regulations and guidelines for data protection\. AWS is responsible for protecting the global infrastructure that runs all the AWS services\. AWS maintains control over data hosted on this infrastructure, including the security configuration controls for handling customer content and personal data\. AWS customers and APN partners, acting either as data controllers or data processors, are responsible for any personal data that they put in the AWS Cloud\.

To manage who can access the Amazon Connect console, you must assign users [security profiles](connect-security-profiles.md)\.

To manage who can access your contact center data through Amazon Connect APIs, we recommend that you use [IAM roles](security-iam.md#security_iam_authentication-iamrole)\. IAM roles have temporary credentials versus the long\-lived credentials for IAM users\. 

We also recommend that you secure your data in the following ways:
+ Use multi\-factor authentication \(MFA\) with each account\.
+ Use SSL/TLS to communicate with AWS resources\.
+ Set up API and user activity logging with AWS CloudTrail\.
+ Use AWS encryption solutions, along with all default security controls within AWS services\.
+ Use advanced managed security services, such as Amazon Macie, which assists in discovering and securing personal data that is stored in Amazon S3\.

We strongly recommend that you never put sensitive identifying information, such as your customers' account numbers, into free\-form fields such as a **Name** field\. This includes when you work with Amazon Connect or other AWS services using the AWS Management Console, API, AWS CLI, or AWS SDKs\. Any data that you enter into Amazon Connect or other services might be included in diagnostic logs\. When you provide a URL to an external server, don't include credentials information in the URL to validate your request to that server\.

For more information about data protection, see the [AWS Shared Responsibility Model and GDPR](http://aws.amazon.com/blogs/security/the-aws-shared-responsibility-model-and-gdpr/) blog post on the AWS Security Blog\.

**Topics**
+ [Data handled by Amazon Connect](data-handled-by-connect.md)
+ [Encryption at rest](encryption-at-rest.md)
+ [Encryption in transit](encryption-in-transit.md)
+ [Key management](key-management.md)