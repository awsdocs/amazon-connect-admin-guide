# Release Notes<a name="amazon-connect-release-notes"></a>

To help you keep rack of the ongoing updates and improvements to Amazon Connect, we're now publishing monthly release notices that describe the changes we've released in the previous month\. Note that we're including both April and May in our first post\.

**Topics**
+ [April and May 2018 Updates](#may18-release-notes)

## April and May 2018 Updates<a name="may18-release-notes"></a>

The following updates were released in April and May 2018:

**Topics**
+ [General Updates](#w3ab1b7b7b7)
+ [Telephony and Voice](#w3ab1b7b7b9)
+ [Contact Flows](#w3ab1b7b7c11)
+ [Metrics](#w3ab1b7b7c13)
+ [Contact Control Panel \(CCP\)](#w3ab1b7b7c15)

### General Updates<a name="w3ab1b7b7b7"></a>
+ New [Amazon Polly voices](http://docs.aws.amazon.com/polly/latest/dg/voicelist.html) are now automatically made available in Amazon Connect as soon as they are launched\. You can use new voices, such as Matthew and Léa, in your contact flows\.
+ Updated password enforcement for Amazon Connect user accounts to match requirements for the Amazon Connect admin account created during instance creation\.
+ Resolved an issue that sometimes resulted in the email addresses not being saved when updating an existing user account\.

### Telephony and Voice<a name="w3ab1b7b7b9"></a>
+ Service optimizations to reduce latency and improve caller ID for Japanese telephony\.
+ Customers can now place calls to Jersey and Guernsey in the Channel Islands\.
+ Added support for keypad numeric input to an Amazon Lex bots when used in an Amazon Connect contact flow\. For more information, see [Amazon Connect Now Supports Keypad Input with an Amazon Lex Chatbot](https://aws.amazon.com/about-aws/whats-new/2018/05/amazon-connect-now-supports-keypad-input-with-an-amazon-lex-chat/)\.
+ Reduced latency for the contact control panel, improving the agent user experience\.

### Contact Flows<a name="w3ab1b7b7c11"></a>
+ Resolved an issue with publishing a contact flow in the case where an **AWS Lambda function block** is used in a contact flow, and the input type for a parameter was changed from **Send attribute** with a **System** attribute is changed to **Send text**\. These contact flows now publish successfully\.
+ Agent and customer whispers are now maintained with queued callbacks\.
+ Attributes now correctly persist with queue callbacks\.
+ Contact attributes are now maintained when using a **Loop prompt** block in a queue flow\.

### Metrics<a name="w3ab1b7b7c13"></a>
+ Data for scheduled reports is now delayed by 15 minutes to allow for most recent data to be incorporated in to reports\. Previously, in some cases, report data for the final 15 minute period during the scheduled report interval did not get included in scheduled reports\. This applies to all report types\.
+ In metric calculations, the time that an incoming call rings is attributed to idle time if the agent is in idle state before an incoming call\.
+ The metric **Agent on contact time** now includes time that an agent spent in an auxiliary busy state\.
+ Published new documentation on [Amazon Connect metrics\.](http://docs.aws.amazon.com/connect/latest/userguide/connect-metrics.html)

### Contact Control Panel \(CCP\)<a name="w3ab1b7b7c15"></a>
+ Added a **Save** button to the settings menu for the CCP when an agent is using a desk phone\. The **Save** button saves the deskphone configuration between sessions\.
+ Agent username is now available as part of agent configuration data in the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md)\. 
+ Contact attributes are now available when using the streams\.js \(Streams API\) for screenpops after queued callbacks\.
+ Fixed issue where for some auto\-accept calls, the agent continued to hear ringing after accepting and joining the call\.