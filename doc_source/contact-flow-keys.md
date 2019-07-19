# Encrypt Customer Input<a name="contact-flow-keys"></a>

You can encrypt sensitive data that is collected by contact flows\. To do this, you need to use public\-key cryptography\. Here's how this works: 

In a contact flow that collects data, you provide an X\.509 certificate to encrypt data that's captured using the **Stored customer input** system attribute\. You must upload a signing key in `.pem` format to use this feature\. The signing key is used to verify the signature of the certificate used within the contact flow\. 

**Note**  
You can have up to two signing keys active at one time to facilitate rotation\.

To decrypt the data in the **Stored customer input** attribute, use the AWS Encryption SDK\. For more information, see the [AWS Encryption SDK Developer Guide](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/)\.

For a detailed walkthrough, see [Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)\. It shows how to:
+ Configure Amazon Connect to collect a credit card number\.
+ Encrypt the credit card digits\.
+ Send it to our backend AWS Lambda for decryption, using the customer supplied decryption key\.