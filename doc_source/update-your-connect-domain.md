# Update your Amazon Connect domain<a name="update-your-connect-domain"></a>

In March 2021 we introduced a new domain name\. Please identify and update any hard\-coded or bookmarked links to pages or APIs\.
+ Previous domain: https://*your\-instance\-alias*\.**awsapps\.com/connect/**
+ New domain: https://*your\-instance\-alias*\.**my\.connect\.aws/**

We are in the process of updating the Amazon Connect console with the new URL\. This change will occur automatically\.

This topic provides information you need to consider when migrating to the new domain\.

## Firewall allow list<a name="new-domain-allow-list"></a>

Add the following new domains to your allow list:
+ \{*your\-instance\-alias*\}\.my\.connect\.aws/ccp\-v2
+ \{*your\-instance\-alias*\}\.my\.connect\.aws/api
+ \*\.static\.connect\.aws

**Important**  
Do not remove the domains already in your allow list:  
\{*your\-instance\-alias*\}\.awsapps\.com/connect/ccp\-v2
\{*your\-instance\-alias*\}\.awsapps\.com/connect/api
\*\.cloudfront\.net

## Transport Layer Security \(TLS\)<a name="new-domain-tls"></a>

Your TLS protocol should be TLS 1\.2\. The new domain does not support TLS 1\.1 and TLS 1\.0\. 

We recommend that you review the new TLS policy: [ALB FS\-1\-2\-Res\-2019\-08](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-https-listener.html#tls-security-policies)\. For reference, you can find the previous TLS policy here: [CloudFront TLSv1](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/secure-connections-supported-viewer-protocols-ciphers.html#secure-connections-supported-ciphers)\. 

## Custom code and integrations<a name="new-domain-custom"></a>

Review and replace hard\-coded references to the previous domain with the new domain\. For example, if you have a custom Contact Control Panel \(CCP\) integration, it likely relies on embedded URLs\. Following are tips for updating this type of integration:
+ Active Directory: If you use Active Directory to manage identity and have an [Amazon Connect managed or customer managed](connect-identity-management.md) instance, then update [ccpUrl](https://github.com/amazon-connect/amazon-connect-streams#connectcoreinitccp) to the new domain\. The next time a user accesses the CCP they will be prompted to login to the new domain \(one time only\)\.
+ SAML 2\.0: If you use SAML 2\.0 to manage identity, then update [ccpUrl](https://github.com/amazon-connect/amazon-connect-streams#connectcoreinitccp) to the new domain, as well as the `loginUrl` to point to your identity provider \(IDP\) to inform when to set the extra `new_domain=true` in the SAML relate state URL\.

## API endpoint access<a name="new-domain-api"></a>

If your team uses hardcoded/bookmarked URLs to access API endpoints, remove '/connect' from those domains\.

For example, if you are using a link that looks like this to access call recordings: 
+  https://*your\-instance\-alias*\.awsapps\.com\_/connect\_/get\-recording

It will change to: 
+  https://*your\-instance\-alias*\.my\.connect\.aws/get\-recording

## Personal settings<a name="new-domain-settings"></a>

Notify your team to the upcoming change so they can take steps to prevent confusion and disruption\. If you have internal documentation that includes links, please review and update accordingly\. Encourage team members to update their browser bookmarks *for the login page*, and productivity apps, such as Alfred\.

To ensure a seamless transition for your team, we encourage you to take steps to identify any missed URL references\.

## Update an old access URL<a name="new-domain-settings"></a>

If you have old instances that were set up with SAML and AWS SSO by using the [pre\-integrated application for Amazon Connect](https://static.global.sso.amazonaws.com/app-20950d6d247fd7bd/instructions/index.htm), then logging in through it goes to the old access URL\. 

To update the URL, add `&new_domain=true` in the old access URL\. The URL will automatically redirect to the new domain\.