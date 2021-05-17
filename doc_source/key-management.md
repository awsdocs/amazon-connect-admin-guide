# Key management<a name="key-management"></a>

You can specify AWS KMS keys, including bring your own keys \(BYOK\), to use for envelope encryption with Amazon S3 input/output buckets\. This also applies to data used stored in Amazon Connect Customer Profiles\.

Amazon AppIntegrations doesn’t support BYOK for encryption of configuration data\.

The knowledge documents used by Amazon Connect Wisdom are encrypted by an AWS KMS key\. 

For information about AWS KMS keys see [What is AWS Key Management Service?](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\.