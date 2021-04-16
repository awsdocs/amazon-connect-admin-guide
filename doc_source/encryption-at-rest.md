# Encryption at rest<a name="encryption-at-rest"></a>

Contact data classified as PII, or data that represents customer content being stored by Amazon Connect, is encrypted at rest using a key that is time\-limited and specific to the Amazon Connect instance\.

Amazon S3 server\-side encryption is used to encrypt conversation recordings \(voice and chat\) and knowledge documents at rest with a KMS data key unique per customer account\. Amazon AppIntegrations configuration data is encrypted the same way\.

Amazon Connect Voice ID stores customer voiceprints which cannot be reverse\-engineered to obtain the enrolled customer’s speech or identify a customer\. These are encrypted using a service\-owned KMS key\.

Integration configuration data is encrypted at rest using a key that is time\-limited and specific to the user account\.

## Amazon Connect Customer Profiles encryption at rest<a name="encryption-at-rest-customer-profiles"></a>

All user data stored in Amazon Connect Customer Profiles is encrypted at rest\. Amazon Connect Customer Profiles encryption at rest provides enhanced security by encrypting all your data at rest using encryption keys stored in AWS Key Management Service \(AWS KMS\)\. This functionality helps reduce the operational burden and complexity involved in protecting sensitive data\. With encryption at rest, you can build security\-sensitive applications that meet strict encryption compliance and regulatory requirements\.

Organizational policies, industry or government regulations, and compliance requirements often require the use of encryption at rest to increase the data security of your applications\. Customer Profiles integrated with AWS KMS to enable its encryption at rest strategy\. For more information, see [AWS Key Management Service Concepts](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html) in the AWS Key Management Service Developer Guide\. 

When creating a new domain, you must provide a CMK that the service will use to encrypt your data in transit and at rest\. The customer managed CMK is created, owned, and managed by you\. You have full control over the CMK \(AWS KMS charges apply\)\.

You can specify an encryption key when you create a new domain or profile object type or switch the encryption keys on an existing resources by using the AWS Command Line Interface \(AWS CLI\), or the Amazon Connect Customer Profiles Encryption API\. When you choose a customer managed CMK, Amazon Connect Customer Profiles creates a grant to the CMK that grants it access to the CMK\.

AWS KMS charges apply for a customer managed CMK\. For more information about pricing, see [AWS KMS pricing](http://aws.amazon.com/kms/pricing/)\. 