# Amazon Connect Contact Control Panel<a name="amazon-connect-contact-control-panel"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to communicate with contacts\. They can use the CCP with a softphone or a desk phone\. 

As the admin, you manage the phone numbers at the instance level, not in the CCP\. For more information, see [Phone Numbers for Your Contact Centers](contact-center-phone-number.md)\. 

## Amazon Connect CCP Concepts<a name="amazon-connect-ccp-concepts"></a>

Amazon Connect provides a number of management and configuration options for your contact center\. The terminology and concepts that are central to your understanding and use of Amazon Connect are described below\.

**agent**  
Users who handle contacts using Amazon Connect\.

**softphone**  
A browser\-based telephony service that is not linked to a handset\. It can be used remotely, provided that the agent is logged in to Amazon Connect\.

**desk phone/handset**  
A physical telephone requiring an agent to be in its proximity in order to make or receive calls\.

**status**  
Metrics are gathered based on changes in agent status \(available, offline, and so on\)\. 

**after contact work**  
A state where the agent is no longer on a call but has related work to complete before being able to accept or make other calls\.

**leave**  
Leave a multi\-party call without disconnecting the other parties or hanging up the call\.

## Access the Amazon Connect CCP<a name="launch-ccp"></a>

As the admin, you can access the CCP by clicking on the phone icon in the upper right corner of Amazon Connect\. 

Before agents can access to the CCP and handle contacts, however, there are a few things you need to do: 
+ Add them as users to the instance\. For more information, see [Manage Users](amazon-connect-instances.md#user-management)\.
+ Configure their permissions\. By default agents assigned to the Agent security profile can access the CCP and make outbound calls\. But you can create a custom security profile and add additional permissions\. For more information, see [Amazon Connect Security Profiles](connect-security-profiles.md)\.
+ Give them their user name, password, and a link to the CCP so they can log in\. The default link is https://*name of your instance*\.awsapps\.com/connect/ccp\#/\.

We recommend telling agents to bookmark the URL to the CCP so they can access it easily\.

## Grant Microphone Access<a name="accessing-microphone"></a>

If agents experience problems with their microphone, they may need to grant microphone access in their browser\.

For Google Chrome steps, see [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)\.

For Mozilla Firefox steps, see [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)\.

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox as your browser\.

## Use E\.164 Format for Telephone Numbers<a name="international-calls-ccp"></a>

Amazon Connect requires phone numbers in [ E\.164](https://www.itu.int/rec/T-REC-E.164/en) format\. E\.164 is an international public telecommunication numbering plan defined by the International Telecommunication Union \(ITU\)\. Using phone numbers in E\.164 format ensures that numbers are interpreted consistently when placing calls between countries, and when phone numbers are passed between software applications and telephony services\.

When you place calls from the CCP using Amazon Connect the CCP provides the correct formatting for numbers automatically\.

E\.164 defines a general format for international telephone numbers\. Numbers are limited to a maximum of 15 digits, excluding the international call prefix\. The presentation of a number is usually prefixed with the plus sign \(\+\), indicating that the number includes the country calling code\. When dialing, the number must typically be prefixed with the appropriate international call prefix \(in place of the plus sign\), which is a trunk code to reach an international circuit from within the country of call origination\. Phone numbers that are not formatted in E\.164 may work, but it depends on the phone or handset that is being used as well as the carrier from which the call is being originated\.

To express a US phone number to E\.164 format, add the '\+' prefix and the country code \(1\) in front of the number\. In the UK and many other countries internationally, local dialing requires the addition of a 0 in front of the subscriber number\. However, to use E\.164 formatting, this 0 must be removed\. A number such as 020 718 xxxxx in the UK would be formatted as \+44 20 718 xxxxx\.

## Set up Softphones and Desk Phones<a name="phone-settings"></a>

Before agents can use the CCP, check the following configurations:
+ **Headset connectivity**—Check the settings in Device Management to ensure that your computer recognizes the headset and allows proper headset connectivity\.
+ **Set up headset**—You may need to adjust your browser settings to ensure correct peripheral selection\.
+ **Desktop notifications**—Ensure that the browser is not in incognito mode so that desktop notifications can be displayed\.
+ **Microphone**—Ensure that the microphone settings are always enabled\.
+ **Dialing**—In **Settings**, you can configure the softphone to dial a DID desk phone if required\. When you choose a desk phone, enter the DID number to which calls go\.

### Softphone CCP IP Address Ranges<a name="ccp-ip-ranges"></a>

If your agents use a softphone for Amazon Connect, you must allow traffic in both directions for the ports and addresses listed below, for the region in which you created your instance\.

The IP addresses used by Amazon Connect for each region are listed, along with the addresses for all AWS services, in the [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json) file under the service name AMAZON\_CONNECT\. For agents to use the CCP, you also need to allow access for the softphone signaling endpoints, which are hosted in Amazon EC2\. For more information about IP address ranges in AWS, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html)\.

When there are new IP address ranges supported for Amazon Connect, they are added to the publicly available [ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json) for a minimum of 30 days before they are used by the service\. After 30 days, softphone traffic through the new IP address ranges increases over the subsequent two weeks\. After two weeks, traffic is routed through the new ranges equivalent to all available ranges\.


| Protocol | Port | Transport Layer | IP Range | 
| --- | --- | --- | --- | 
| HTTP | 80 | TCP | AWS EC2 and CLOUDFRONT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 
| HTTPS | 443 | TCP | AWS EC2 and CLOUDFRONT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 
| TURN | 3478 | UDP | AMAZON\_CONNECT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 

### Status Settings<a name="status"></a>

The status settings are used for reporting purposes to ensure that system issues are resolved quickly and to manage resources\.

The following settings are available:
+ **Available**—Indicates that an agent is available to take calls\.
+ **Offline**—Logs agents out and removes them from the pool of available agents\.

## Application Integration<a name="app-integration"></a>

All domains that embed the CCP for a particular instance must be explicitly whitelisted for cross\-domain access to the instance\. For example, to integrate with Salesforce, you must whitelist your Salesforce Visualforce domain\.

**To whitelist a domain URL**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the name of the instance from **Instance Alias**\.

1. In the navigation pane, choose **Application integration**\.

1. Choose **Add origin**\.

1. Type the URL and choose **Add**\.