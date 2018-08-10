# Release Notes<a name="amazon-connect-release-notes"></a>

To help you keep track of the ongoing updates and improvements to Amazon Connect, we're now publishing monthly release notices that describe the changes we've released in the previous month\.

**Topics**
+ [June 2018 Updates](#jun18-release-notes)
+ [April and May 2018 Updates](#may18-release-notes)

## June 2018 Updates<a name="jun18-release-notes"></a>

The following updates were released in June 2018:

**Topics**
+ [General Updates](#june-general)
+ [Telephony and Voice](#june-telephony)
+ [Contact Flows](#june-contact-flows)
+ [Metrics](#june-metrics)
+ [Contact Control Panel \(CCP\)](#june-ccp)

### General Updates<a name="june-general"></a>
+ Changed the font in the UI to Amazon Ember for better readability\.

### Telephony and Voice<a name="june-telephony"></a>
+ Introduced support for using Amazon Lex bots with Amazon Connect in the US West \(Oregon\) Region\.
+ Fixed a bug that in some cases caused a call to drop when a Loop prompt occurred at the same as a call connecting to an agent\.

### Contact Flows<a name="june-contact-flows"></a>
+ Renamed the **Set queue** block to **Set working queue**\.
+ Added a **Copy to clipboard** button next to the ARN of a contact flow so you can easily copy the ARN\. Choose **Show additional flow information** under the name of the contact flow in the designer to display the ARN\.
+ Added a new **Call phone number** block, which lets you choose the phone number from your instance to display as the caller ID in an outbound whisper flow\. For more information, see [Using a Call phone number block in a contact flow](http://docs.aws.amazon.com/connect/latest/userguide/contactflow.html#using-call-number-block)\.
+ Released contact attributes for system metrics, including a new **Get metrics** block in contact flows\. For more information, see [Using System Metric Attributes](http://docs.aws.amazon.com/connect/latest/userguide/contact-attributes.html#attrib-system-metrics)\.

### Metrics<a name="june-metrics"></a>
+ Fixed an issue that caused incorrect rendering of the search field in the filters settings for some historical metrics reports\.
+ Fixed an issue in downloaded reports where the phone number would be blank instead of listing the phone number for calls that were callbacks\.
+ Login/Logout reports now support 20,000 rows per report generation, up from 10,000\.

### Contact Control Panel \(CCP\)<a name="june-ccp"></a>
+ Added a mute button to the CCP and a mute function to the Streams API so agents can mute and unmute active calls\.

## April and May 2018 Updates<a name="may18-release-notes"></a>

The following updates were released in April and May 2018:

**Topics**
+ [General Updates](#may-general)
+ [Telephony and Voice](#may-telephony)
+ [Contact Flows](#may-contact-flows)
+ [Metrics](#may-metrics)
+ [Contact Control Panel \(CCP\)](#may-ccp)

### General Updates<a name="may-general"></a>
+ New [Amazon Polly voices](http://docs.aws.amazon.com/polly/latest/dg/voicelist.html) are now automatically made available in Amazon Connect as soon as they are launched\. You can use new voices, such as Matthew and Léa, in your contact flows\.
+ Updated password enforcement for Amazon Connect user accounts to match requirements for the Amazon Connect admin account created during instance creation\.
+ Resolved an issue that sometimes resulted in the email addresses not being saved when updating an existing user account\.

### Telephony and Voice<a name="may-telephony"></a>
+ Service optimizations to reduce latency and improve caller ID for Japanese telephony\.
+ Customers can now place calls to Jersey and Guernsey in the Channel Islands\.
+ Added support for keypad numeric input to an Amazon Lex bots when used in an Amazon Connect contact flow\. For more information, see [Amazon Connect Now Supports Keypad Input with an Amazon Lex Chatbot](https://aws.amazon.com/about-aws/whats-new/2018/05/amazon-connect-now-supports-keypad-input-with-an-amazon-lex-chat/)\.
+ Reduced latency for the contact control panel, improving the agent user experience\.

### Contact Flows<a name="may-contact-flows"></a>
+ Resolved an issue with publishing a contact flow in the case where an **AWS Lambda function block** is used in a contact flow, and the input type for a parameter was changed from **Send attribute** with a **System** attribute is changed to **Send text**\. These contact flows now publish successfully\.
+ Agent and customer whispers are now maintained with queued callbacks\.
+ Attributes now correctly persist with queue callbacks\.
+ Contact attributes are now maintained when using a **Loop prompt** block in a queue flow\.

### Metrics<a name="may-metrics"></a>
+ Data for scheduled reports is now delayed by 15 minutes to allow for most recent data to be incorporated in to reports\. Previously, in some cases, report data for the final 15 minute period during the scheduled report interval did not get included in scheduled reports\. This applies to all report types\.
+ In metric calculations, the time that an incoming call rings is attributed to idle time if the agent is in idle state before an incoming call\.
+ The metric **Agent on contact time** now includes time that an agent spent in an auxiliary busy state\.
+ Published new documentation on [Amazon Connect metrics\.](http://docs.aws.amazon.com/connect/latest/userguide/connect-metrics.html)

### Contact Control Panel \(CCP\)<a name="may-ccp"></a>
+ Added a **Save** button to the settings menu for the CCP when an agent is using a desk phone\. The **Save** button saves the deskphone configuration between sessions\.
+ Agent username is now available as part of agent configuration data in the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md)\. 
+ Contact attributes are now available when using the streams\.js \(Streams API\) for screenpops after queued callbacks\.
+ Fixed issue where for some auto\-accept calls, the agent continued to hear ringing after accepting and joining the call\.