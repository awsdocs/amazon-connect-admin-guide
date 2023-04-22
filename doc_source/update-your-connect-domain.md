# Update your Amazon Connect domain<a name="update-your-connect-domain"></a>

We are in the process of updating the Amazon Connect console with a new URL: 
+  https://*your\-instance\-alias*\.**my\.connect\.aws/**

**This change will occur automatically**\. 

**Note**  
To prepare for this change, you need to change any **hardcoded** or **bookmarked** links\. If your old link looks like this:  
https://*your\-instance\-alias*\.**awsapps\.com/connect/**
**Change to:**  
https://*your\-instance\-alias*\.**my\.connect\.aws/**

In addition, there are other steps you will need to take if you use a firewall, SAML, or other connectors such as Salesforce\. This topic provides information you need to consider when migrating to the new domain\.

**Topics**
+ [Firewall allow list](#new-domain-allow-list)
+ [Transport Layer Security \(TLS\)](#new-domain-tls)
+ [Custom code and integrations](#new-domain-custom)
+ [API endpoint access](#new-domain-api)
+ [Personal settings](#new-domain-settings)

## Firewall allow list<a name="new-domain-allow-list"></a>

Add the following new domains to your allow list:
+ *your\-instance\-alias*\.my\.connect\.aws/ccp\-v2
+ *your\-instance\-alias*\.my\.connect\.aws/api
+ \*\.static\.connect\.aws

**Important**  
Do not remove the domains already in your allow list:  
*your\-instance\-alias*\.awsapps\.com/connect/ccp\-v2
*your\-instance\-alias*\.awsapps\.com/connect/api
\*\.cloudfront\.net

For more information about setting up your allow list, see [Set up your network](ccp-networking.md)\.

## Transport Layer Security \(TLS\)<a name="new-domain-tls"></a>

Your TLS protocol should be TLS 1\.2\. The new domain does not support TLS 1\.1 and TLS 1\.0\. 

We recommend that you review the new TLS policy: [ALB FS\-1\-2\-Res\-2019\-08](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-https-listener.html#tls-security-policies)\. For reference, you can find the previous TLS policy here: [CloudFront TLSv1](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/secure-connections-supported-viewer-protocols-ciphers.html#secure-connections-supported-ciphers)\. 

## Custom code and integrations<a name="new-domain-custom"></a>

Review and replace hard\-coded references to the previous domain with the new domain\. For example, if you have a custom Contact Control Panel \(CCP\) integration, it likely relies on embedded URLs\. Following are tips for updating this type of integration\.

### Active Directory<a name="new-domain-ad"></a>

If you use Active Directory to manage identity and have an [Amazon Connect managed or customer managed](connect-identity-management.md) instance, then update [ccpUrl](https://github.com/amazon-connect/amazon-connect-streams#connectcoreinitccp) to the new domain\. The next time a user accesses the CCP they will be prompted to login to the new domain \(one time only\)\.

### SAML 2\.0<a name="new-domain-saml"></a>

If you use SAML 2\.0 to manage identity, then do the following steps: 
+ Update `ccpUrl` in your [Amazon Connect Streams](https://github.com/amazon-connect/amazon-connect-streams#connectcoreinitccp) to the new domain `your-instance-alias.my.connect.aws/ccp-v2`\.
+ When you configure the relay state for your identity provider, update the `loginUrl` with `new_domain=true`\.
+ You must use [URL encoding](https://en.wikipedia.org/wiki/Percent-encoding) for the destination and new\_domain in the URL\.

If you have old instances that were set up with SAML, do the following steps:

1. If `loginUrl` contains `destination=%2Fconnect%2Fyour-destination-endpoint`, remove the `%2Fconnect` endpoint prefix from the new domain destination\.

1. Add `new_domain=true` before or after `destination=%2Fyour-destination-endpoint`\. It should be separated by `%26`\.

1. If `loginUrl` does not contain destination or any other parameter, add `?new_domain=true` after the relay state URL\.

Following are examples of valid relay state URLs:
+ `https://us-east-1.console.aws.amazon.com/connect/federate/your-instance-id?destination=%2Fccp-v2%2Fchat%26new_domain=true`
+ `https://us-east-1.console.aws.amazon.com/connect/federate/your-instance-id?new_domain=true`

### Other connectors<a name="new-domain-saml"></a>

If you use Salesforce, Zendesk, ServiceNow, or other connectors: 

1. Upgrade to the latest version of your connector\.

1. In your connector, go to the settings and update the Amazon Connect domain that is stored there\. Follow the SAML tips if applicable\.

## API endpoint access<a name="new-domain-api"></a>

If your team uses hardcoded/bookmarked URLs to access API endpoints, remove '/connect' from those domains, and change the URL to *your\-instance\-alias*\.my\.connect\.aws\.

For example, if you are using a link that looks like this to access call recordings: 
+  https://*your\-instance\-alias*\.awsapps\.com\_/connect\_/get\-recording

Change the link to: 
+  https://*your\-instance\-alias*\.my\.connect\.aws/get\-recording

## Personal settings<a name="new-domain-settings"></a>

Notify your team to the upcoming change so they can take steps to prevent confusion and disruption\. If you have internal documentation that includes links, please review and update accordingly\. Encourage team members to update their browser bookmarks *for the login page*, and productivity apps, such as Alfred\.

To ensure a seamless transition for your team, we encourage you to take steps to identify any missed URL references\.