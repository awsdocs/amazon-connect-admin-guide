# Infrastructure security in Amazon Connect<a name="infrastructure-security"></a>

As a managed service, Amazon Connect is protected by the AWS global network security procedures that are described on the [ Best Practices for Security, Identity, and Compliance](http://aws.amazon.com/architecture/security-identity-compliance/) page\. 

You use AWS published API calls to access Amazon Connect through the network\.

## Supported versions of TLS<a name="supported-version-tls"></a>

Clients must support Transport Layer Security \(TLS\) 1\.2 or later\. 

Amazon Connect offers a new website access model with a new domain \(instance name\.my\.connect\.aws\) that supports TLS 1\.2 or newer versions only\. It is available by default for instances created after March 2021\. Existing customers can opt in to using the new domain using the following methods: 
+ For non\-SAML Amazon Connect instances, change your access URL from **\.awsapps\.com/connect** to **\.my\.connect\.aws** and log in again\.
+ For SAML\-enabled instances, specify an extra query parameter new\_domain=true in the relay state URL and log in again\. For more information, see [Use a destination in your relay state URL](configure-saml.md#destination-relay)\. 

## Other requirements<a name="client-access-key-requirements"></a>

Clients must support cipher suites with perfect forward secrecy \(PFS\) such as Ephemeral Diffie\-Hellman \(DHE\) or Elliptic Curve Ephemeral Diffie\-Hellman \(ECDHE\)\. Most modern systems such as Java 7 and later support these modes\.

Additionally, requests must be signed by using an access key ID and a secret access key that is associated with an IAM principal\. Or you can use the [AWS Security Token Service](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html) \(AWS STS\) to generate temporary security credentials to sign requests\.

You can call these API operations from any network location, but Amazon Connect does support resource\-based access policies, which can include restrictions based on the source IP address\. 