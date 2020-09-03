# Infrastructure security in Amazon Connect<a name="infrastructure-security"></a>

As a managed service, Amazon Connect is protected by the AWS global network security procedures that are described in the [Amazon Web Services: Overview of Security Processes](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Whitepaper.pdf) whitepaper\.

You use AWS published API calls to access Amazon Connect through the network\.

## Supported versions of TLS<a name="supported-version-tls"></a>

Clients must support Transport Layer Security \(TLS\) 1\.2 or later\. 

## Other requirements<a name="client-access-key-requirements"></a>

Clients must support cipher suites with perfect forward secrecy \(PFS\) such as Ephemeral Diffie\-Hellman \(DHE\) or Elliptic Curve Ephemeral Diffie\-Hellman \(ECDHE\)\. Most modern systems such as Java 7 and later support these modes\.

Additionally, requests must be signed by using an access key ID and a secret access key that is associated with an IAM principal\. Or you can use the [AWS Security Token Service](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html) \(AWS STS\) to generate temporary security credentials to sign requests\.

You can call these API operations from any network location, but Amazon Connect does support resource\-based access policies, which can include restrictions based on the source IP address\. 