# Provide Access to the Contact Control Panel<a name="amazon-connect-contact-control-panel"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to communicate with contacts\. But before agents can access to the CCP and handle contacts, there are a few things you need to do: 
+ Add them as users to the instance\. For more information, see [Manage Users in Amazon Connect](manage-users.md)\.
+ Configure their permissions\. By default agents assigned to the Agent security profile can access the CCP and make outbound calls\. But you can create a custom security profile and add additional permissions\. For more information, see [Security Profiles](connect-security-profiles.md)\.
+ Give them their user name, password, and a link to the CCP so they can log in\. The default link is https://*name of your instance*\.awsapps\.com/connect/ccp\#/\.

We recommend telling agents to bookmark the URL to the CCP so they can access it easily\.

As the admin, you can access the CCP by clicking on the phone icon in the upper right corner of Amazon Connect\.

## Grant Microphone Access in Chrome or Firefox<a name="accessing-microphone"></a>

If agents experience problems with their microphone, they may need to grant microphone access in their browser\.

For Google Chrome steps, see [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)\.

For Mozilla Firefox steps, see [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)\.

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox as your browser\.

For help solving problems with hearing a conversation, see [Set up Softphones and Desk Phones](#phone-settings)\. 

## Use E\.164 Format for Telephone Numbers<a name="international-calls-ccp"></a>

Amazon Connect requires phone numbers in [ E\.164](https://www.itu.int/rec/T-REC-E.164/en) format\. E\.164 is an international public telecommunication numbering plan defined by the International Telecommunication Union \(ITU\)\. Using phone numbers in E\.164 format ensures that numbers are interpreted consistently when placing calls between countries, and when phone numbers are passed between software applications and telephony services\.

When you place calls from the CCP using Amazon Connect the CCP provides the correct formatting for numbers automatically\.

E\.164 defines a general format for international telephone numbers\. Numbers are limited to a maximum of 15 digits, excluding the international call prefix\. The presentation of a number is usually prefixed with the plus sign \(\+\), indicating that the number includes the country calling code\. When dialing, the number must typically be prefixed with the appropriate international call prefix \(in place of the plus sign\), which is a trunk code to reach an international circuit from within the country of call origination\. Phone numbers that are not formatted in E\.164 may work, but it depends on the phone or handset that is being used as well as the carrier from which the call is being originated\.

To express a US phone number to E\.164 format, add the '\+' prefix and the country code \(1\) in front of the number\. In the UK and many other countries internationally, local dialing requires the addition of a 0 in front of the subscriber number\. However, to use E\.164 formatting, this 0 must be removed\. A number such as 020 718 xxxxx in the UK would be formatted as \+44 20 718 xxxxx\.

## Set up Softphones and Desk Phones<a name="phone-settings"></a>

Before agents can use the CCP, or if they are having problems hearing a conversation or being heard, check the following:
+ **Headset connectivity**—Check the settings in Device Management to ensure that your computer recognizes the headset and allows proper headset connectivity\.
+ **Set up headset**—You may need to adjust your browser settings to ensure correct peripheral selection\.
+ **Desktop notifications**—Ensure that the browser is not in incognito mode so that desktop notifications can be displayed\.
+ **Microphone**—Ensure that the microphone settings are always enabled\.
+ **Dialing**—In **Settings**, you can configure the softphone to dial a DID desk phone if required\. When you choose a desk phone, enter the DID number to which calls go\.