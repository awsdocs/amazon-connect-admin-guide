# Amazon Connect Contact Control Panel<a name="amazon-connect-contact-control-panel"></a>

Agents use the Amazon Connect Contact Control Panel \(CCP\) to communicate with contacts\. The CCP can be used with a softphone or a desk phone\. The phone number and configurations are managed in Amazon Connect\.

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

## Launch the Amazon Connect CCP<a name="launch-ccp"></a>

You can log in to the CCP using the link provided by the Amazon Connect administrator\. We recommend that you bookmark the URL for easy access\. After you are logged in, choose the phone icon to open the CCP\.

## Set up Users and Permissions<a name="ccp-permissions"></a>

Before agents can use the CCP to take calls, you configure permissions\. These permissions are edited in Amazon Connect, and cover a range of activities from generating reports to making calls\. The permissions also ensure that agents only see, and have access to, what's relevant to their job\.

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

Agents can log in using the URL, user name, and password provided by their Amazon Connect administrator\. Each agent has a unique user name and password\.

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

## Work with Calls<a name="working-with-calls"></a>

Using the Contact Control Panel \(CCP\), you can perform the following actions on a softphone\. When you opt for a desk phone, you have the same controls as softphone\. The only difference is that there is no **Accept** button on a desk phone\.

**Accepting incoming calls**
+ To accept an incoming call, choose **Accept call**\.
+ To edit settings, choose **Settings**\.
+ To end a call, choose **End call**\.
+ To put a call on hold, choose **Hold**\.

When a call is connected, a new set of options become available in the CCP\.

**Transfers**

After an agent picks up a call, the agent can transfer the call by choosing the **Transfer** button and then choosing one of the available contacts\. The contacts displayed are the quick connects defined in your Amazon Connect instance, which have been added to a queue in the agent's routing profile and are associated with a contact flow that support call transfers\.

Agents can also manually enter a phone number to transfer calls to by choosing **Dial number** after answering the call\. The agent can enter a phone number using the keypad, and then choose **Transfer** to transfer the call\. If agents regularly transfer calls to a specific phone number, you can create an **External** contact flow and use that phone number for the destination\.

**To enable agent call transfers**

1. Create and publish a contact flow for the type of transfer to enable\.
   + To enable transfers to another agent, create a Transfer to agent contact flow\.
   + To enable transfers to a queue, create a Transfer to queue contact flow\.
   + External transfers do not require a specific type of contact flow\.
**Note**  
You must publish your contact flows to make them active in your contact center\.

1. Create a quick connect for the type of transfer to enable: **Agent**, **Queue**, or **External**\.

   When you create the **Agent** or **Queue** quick connect, select a contact flow that matches the type of transfer to enable\. **External** quick connects require only a phone number, and do not allow you to set a queue or contact flow\.

   For more information about quick connects, see [Create Quick Connects](connect-contact-flows.md#quick-connects)\.

1. Add the quick connect that you created to any queue used in a contact flow for which to enable call transfer, such as the queue used in the contact flow for incoming calls\. The queue must be in the routing profile assigned to the agent who should be able to transfer calls\. The quick connects are displayed in the list of contacts when an agent tries to transfer an active call\.

**To transfer calls to an agent or queue**

1. After accepting a call in the CCP, choose **Transfer**\.

1. Select the contact to whom to transfer the call, and then choose **Dial**\.

   The call is placed on hold during the transfer\.

1. After the call is answered by an agent, or sent to a queue, choose **Leave call** to disconnect from the call\.

1. To use conference, swap, or hold:
+ To begin a conference call, choose **Join** to perform a soft transfer\. To drop out of the call, choose **Leave**\.
+ Choose **Swap** to switch between talking to a customer and the person to whom you’re transferring the call\.
+ Choose **Hold all** to put all parties on hold\.

Some settings that are configured in Amazon Connect include setting agents to go into the `After call work` state after they are done with their call\. Agents can also be configured to accept a call automatically, without having to choose **Accept**\.

### Granting Microphone Access<a name="accessing-microphone"></a>

If you're experiencing problems with your microphone, you may need to grant microphone access in your browser\.

For Google Chrome steps, see [Use your camera and microphone in Chrome](https://support.google.com/chrome/answer/2693767?hl=en)\.

For Mozilla Firefox steps, see [Firefox Page Info window](https://support.mozilla.org/en-US/kb/firefox-page-info-window)\.

**Important**  
A change introduced in Google Chrome version 64 may result in issues with receiving calls if you are using an embedded Contact Control Panel \(CCP\) softphone using the Amazon Connect Streams library\. If you are experiencing issues with your microphone when using Chrome version 64, you can resolve the issue by building and deploying the latest version of the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md#downloading-streams), following the steps under *Downloading Streams*\.  
You can also resolve the issue by using Firefox as your browser\.

## How to Enable Manager Listen\-in<a name="manager-listen-in"></a>

As a manager, you can listen in on active calls as your agents interact with your customers\. Only users that are assigned the **Enable** permissions for **Manager listen in** can listen in on agent calls\. The **CallCenterManager** security profile includes this permission, but not permission to access the CCP\. You can add the permission for the CCP to the **CallCenterManager** profile, or also assign the **Agent** profile to an account that is already assigned the **CallCenterManager** profile\.

Before you can use the listen\-in feature, you need to enable call recording in your contact flows\. The listen\-in feature works only when call recording is enabled\. To enable Manager listen\-in for outbound calls, the contact flow in which you enable call recording must be in the flow selected as the outbound contact flow for the queue used for outbound calls\.

**To enable manager listen\-in**

1. Log in to your Amazon Connect instance using an account that has permissions to edit contact flows\.

1. Identify a contact flow that handles customer contacts that you want to listen in on\.

1. Choose **Routing**, **Contact flows**, and then choose the name of the contact flow to open it in the editor\.

1. Add a **Set call recording behavior** block to the contact flow, select **Agent and Customer** under **Record**, and then choose **Save**\.

   Call recording must be enabled before the call being connected to an agent\.
**Important**  
Make sure that the block has connections to the block before and after it in the contact flow\.

1. Choose **Save and Publish** to publish the updated contact flow\. Choose **Save and Publish** again to confirm that you want to overwrite the published version\.

**To listen in on agent calls**

1. Log in to your Amazon Connect instance with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Manager listen in** permission\.

1. Open the CCP by choosing the phone icon in the top\-right corner of the screen\.

1. Choose **Metrics and quality**, **Real\-time metrics**\.

1. On the **Real\-time metrics** page, choose **Agents**\.

   For any agent that is on a call, there is a headset icon next to the agent's login name\. Choose the icon to start listening to the call\.

   When you are listening to call, the status in your contact control panel changes to **Monitoring**\.

1. To stop listening to the call, choose **End call**\.

   When the agent ends the call, monitoring stops automatically\.