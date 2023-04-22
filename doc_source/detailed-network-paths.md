# Detailed network paths for Amazon Connect<a name="detailed-network-paths"></a>

## Voice calls<a name="detailed-network-paths-voice"></a>

The following diagram shows how voice calls flow through Amazon Connect 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/network-path-voice-calls.png)

1. Users access the Amazon Connect application using a web browser\. All communications are encrypted in transit using TLS\.

1. Users establish voice connectivity to Amazon Connect from their browser using WebRTC\. Signaling communication is encrypted in transit using TLS\. Audio is encrypted in transit using SRTP\.

1. Voice connectivity to traditional phones \(PSTN\) is established between Amazon Connect and AWS telecommunications carrier partners using private network connectivity\. In cases where shared network connectivity is used, signaling communication is encrypted in transit using TLS and audio is encrypted in transit using SRTP\.

1. Call recordings are stored in your Amazon S3 bucket that Amazon Connect has been given permissions to access\. This data is encrypted between Amazon Connect and Amazon S3 using TLS\.

1. Amazon S3 server\-side encryption is used to encrypt call recordings at rest using a customer\-owned KMS key\.

## Authentication<a name="detailed-network-paths-authentication"></a>

The following diagram shows using the AD Connector with AWS Directory Service to connect to an existing customer Active Directory installation\. The flow is similar to using AWS Managed Microsoft AD\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/network-path-authentication.png)

1. The user's web browser initiates authentication to an OAuth gateway over TLS using the public internet with user credentials \(Amazon Connect login page\)\.

1. OAuth gateway sends the authentication request over TLS to AD Connector\.

1. AD Connector does LDAP authentication to Active Directory\.

1. The user's web browser receives OAuth ticket back from gateway based on authentication request\.

1. The client loads the Contact Control Panel \(CCP\)\. The request is over TLS and uses OAuth ticket to identify user/directory\.