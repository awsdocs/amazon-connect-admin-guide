# Key management<a name="key-management"></a>

You can specify AWS KMS keys, including bring your own keys \(BYOK\), to use for envelope encryption with Amazon S3 input/output buckets\. This also applies to data used stored in Amazon Connect Customer Profiles\.

Amazon Connect Wisdom stores knowledge documents that are encrypted at rest in S3 using a BYOK or a service\-owned key\. The knowledge documents are encrypted at rest in Amazon OpenSearch Service using a service\-owned key\. Wisdom stores agent queries and call transcripts using a BYOK or a service\-owned key\.

Amazon AppIntegrations doesn’t support BYOK for encryption of configuration data\. When syncing external application data, periodically you are required to BYOK\. Amazon AppIntegrations requires a grant to use your customer managed key\. When you create a data integration, Amazon AppIntegrations sends a `CreateGrant` request to AWS KMS on your behalf\. You can revoke access to the grant, or remove the service's access to the customer managed key at any time\. If you do, Amazon AppIntegrations won't be able to access any of the data encrypted by the customer managed key, which affects Amazon Connect services that are dependent on that data\.

The knowledge documents used by Amazon Connect Wisdom are encrypted by an AWS KMS key\. 

 For using Amazon Connect Voice ID, it is mandatory to provide a customer managed key KMS key \(BYOK\) while creating a Amazon Connect Voice ID domain, which is used to encrypt all the customer data at rest\. 

Outbound campaigns encrypts all sensitive data using an AWS owned key or a customer managed key\. As the customer managed key is created, owned, and managed by the you, you have full control over the customer managed key \(AWS KMS charges apply\)\.

For information about AWS KMS keys see [What is AWS Key Management Service?](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\.