# Release Notes<a name="amazon-connect-release-notes"></a>

To help you keep track of the ongoing updates and improvements to Amazon Connect, we publish release notices that describe recent changes\.

**Topics**
+ [February 2020 Update](#feb20-release-notes)
+ [January 2020 Update](#jan20-release-notes)
+ [December 2019 Update](#dec19-release-notes)
+ [November 2019 Update](#nov19-release-notes)
+ [October 2019 Update](#oct19-release-notes)
+ [June 2019 Update](#w50aac60c17)
+ [May 2019 Updates](#w50aac60c19)
+ [April 2019 Updates](#w50aac60c21)
+ [March 2019 Update](#w50aac60c23)
+ [February 2019 Updates](#feb19-release-notes)
+ [January 2019 Updates](#jan19-release-notes)
+ [December 2018 Updates](#dec18-release-notes)
+ [November 2018 Updates](#nov18-release-notes)
+ [October 2018 Updates](#oct18-release-notes)
+ [September 2018 Updates](#sep18-release-notes)
+ [August 2018 Updates](#aug18-release-notes)
+ [July 2018 Updates](#july18-release-notes)
+ [June 2018 Updates](#jun18-release-notes)
+ [April and May 2018 Updates](#may18-release-notes)

## February 2020 Update<a name="feb20-release-notes"></a>

The following updates were released in February 2020:

### Service Quotas<a name="feb20-networking"></a>
+ Adjusted [Amazon Connect Service Quotas](amazon-connect-service-limits.md) for new accounts\.

### Contact Flows<a name="feb20-contact-flows"></a>

Updated the following blocks so you can set contact attributes:
+ [Set Customer Queue Flow](set-customer-queue-flow.md)
+ [Set Hold Flow](set-hold-flow.md) 
+ [Set Whisper Flow](set-whisper-flow.md) 

## January 2020 Update<a name="jan20-release-notes"></a>

The following updates were released in January 2020:

### Contact Control Panel \(CCP\)<a name="jan20-ccp"></a>

The following updates were made to the updated Contact Control Panel \(ccp\-v2\):
+ Agents can now transfer a contact by double\-clicking a quick connect\. For more information, see [Initiate a Quick Connect Transfer](transfers.md#transfers-quick)\.
+ The number pad now retains the previously selected country flag so agents don't need to select it every time\.
+ All strings in the CCP user interface are now localized in available languages\.
+ Resolved an issue where the color of the call status bar incorrectly displayed as green during a conference call when the call was in the Joined state\. It is now blue\.
+ Resolved an issue where the agent’s name was displayed in error messages for missed chats, rather than the customer’s name\.

### Networking<a name="jan20-networking"></a>
+ Updated [Set Up Your Network](ccp-networking.md) to include requirements for the updated Contact Control Panel \(ccp\-v2\)\.

## December 2019 Update<a name="dec19-release-notes"></a>

The following update was released in December 2019:

### Monitoring<a name="dec19-monitoring"></a>
+ Added Contact Lens for Amazon Connect\. This feature enables you search conversations for keywords, sentiment scores, and non\-talk time\. For more information, see [Analyze Conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\.
+ Added logging of Amazon Connect API calls with AWS CloudTrail\. For more information, see [Logging Amazon Connect API Calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

## November 2019 Update<a name="nov19-release-notes"></a>

The following updates were released in November 2019:

### Omnichannel Support<a name="nov19-channel"></a>
+ Added support for chat communications\. For more information, see [Concepts](connect-concepts.md)\. 

### Metrics<a name="nov19-metrics"></a>
+ For a description of changes, see [What's New in Metrics](upcoming-changes.md)\.

### Contact Flows<a name="nov19-contact-flows"></a>

Added the following contact flow blocks:
+ [Contact Block: Wait](wait.md)
+ [Contact Block: Set Disconnect Flow](set-disconnect-flow.md) 

Updated the following contact flow blocks for chat:
+ [Contact Block: Play Prompt](play.md)
+ [Contact Block: Get Customer Input](get-customer-input.md)
+ [Contact Block: Store Customer Input](store-customer-input.md)
+ [Contact Block: Set Recording Behavior](set-recording-behavior.md)

### User Management<a name="nov19-users"></a>
+ Added that you can use AWS Identity and Access Management \(IAM\) with Amazon Connect\. For more information, see [Identity and Access Management for Amazon Connect](security-iam.md)\.

### Live Media Streaming<a name="nov19-lms"></a>
+ Added that you can capture customer audio for the entire interaction with your contact center\. For more information, see [Capture Customer Audio: Live Media Streaming](customer-voice-streams.md)\.

### API<a name="nov19-api"></a>
+ Added [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html), [ListTagsForResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListTagsForResource.html), [TagResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_TagResource.html), [UntagResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_UntagResource.html) to the Amazon Connect Service API\.
+ Added the [Amazon Connect Participant Service](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html) API\. These APIs are used chat participants, such as agents and customers\.

### Contact Control Panel \(CCP\)<a name="nov19-CCP"></a>
+ Updated the CCP so it supports chat\. For more information, see [Using the CCP \(the Agent UI\)](agent-user-guide.md)\. 

## October 2019 Update<a name="oct19-release-notes"></a>

The following update was released in October 2019:

### Metrics<a name="oct19-metrics"></a>
+ The real time metric **On call** is now incremented whenever an agent is handling a contact who is connected, on hold, in After Contact Work, or the agent is dialog out to a customer\. 

  This metric is available in the Queues tables and Routing Profile tables on the **Real time metrics** page\. It's also returned by the `GetCurrentMetricData` API as `AGENTS_ON_CALL`\. 

## June 2019 Update<a name="w50aac60c17"></a>

The following update was released in June 2019:

### Contact Flows<a name="june19-flows"></a>
+ Added contact flow versioning so you can choose between a saved or published version when you roll back\.

## May 2019 Updates<a name="w50aac60c19"></a>

The following updates were released in May 2019:

### Metrics and Reporting<a name="may19-flows"></a>
+ Improved the error messages you might encounter when creating, editing, or deleting a scheduled report\. 
+ In the Historical metrics report UI, changed **Contacts missed** to **Agent non\-response**\. This metric appears as **Contacts missed** in scheduled reports and exported CSV files\.
+ In the agent event stream, fixed the formatting of the timestamp millisecond so you can better order and analyze the data\. To learn more, see [Amazon Connect Agent Event Streams](agent-event-streams.md)\. 

### Contact Control Panel<a name="may19-ccp"></a>
+ Resolved an issue where calling a destroy action \(such as `connection.destroy`\) using the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md) resulted in different behavior depending on which leg of the conversation it was called from: the agent or the customer\. Now calling a destroy action results in the same behavior for both: a busy conversation is moved to After Call Work \(ACW\) and a conversation in any other state is cleared\. If you used the native Contact Control Panel instead of the Amazon Connect Streams API, you weren't impacted by this issue\.

## April 2019 Updates<a name="w50aac60c21"></a>

The following updates were released in April 2019:

### Contact Control Panel<a name="april19-ccp"></a>
+ Resolved an issue where the hold flow didn't run in this case: 
  + The agent missed a call and then set themselves back to Available\.
  + Then they were re\-routed the same call\.
  + The agent put that customer on hold while handling the call\.

  However, taking the customer off hold worked as expected and no other impact occurred\.
+ Resolved an issue where the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md) returned `softphoneAutoAccept = FALSE` even though **Auto\-Accept Call** was enabled for the agent\. 

## March 2019 Update<a name="w50aac60c23"></a>

The following updates were released in March 2019:

### Metrics and Reporting<a name="march19-flows"></a>
+ Improved the error messages you might encounter when running real\-time metrics reports\. For example, if you manually configure a real\-time metrics report to contain more than 100 queues, we'll display this message: "You've hit the maximum limit of 100 queues\. Please reconfigure your report to contain no more than 100 queues\." To learn more, see [No Metrics or Too Few Rows in a Queues Report?](troubleshoot-rtm.md)

### Contact Control Panel<a name="march19-ccp"></a>
+ Resolved an issue where, in rare cases, an agent already handling an outbound call could have been incorrectly presented with an additional queued callback, even though they are only allowed to handle one contact at a time\. Since that agent would have been on contact and not idle, the agent wouldn't have been able to accept the queued callback\.

  In these cases, the outbound call was not impacted; the agent wouldn't have noticed any differences in the CCP\. The callback was presented to another agent instead of being dropped\.

## February 2019 Updates<a name="feb19-release-notes"></a>

The following updates were released in February 2019:

**Topics**
+ [Contact Routing](#feb19-contact-routing)
+ [Contact Flows](#feb19-flows)
+ [Metrics and Reporting](#feb19-metrics)
+ [Contact Control Panel \(CCP\)](#feb19-ccp)

### Contact Routing<a name="feb19-contact-routing"></a>
+ Resolved an issue where in rare cases some contacts were not routed to the agent that was available for the longest time\.
+ Resolved an issue in the user interface where the value displayed for **No\. of agents staffed** for the **Basic Routing Profile** on the **Routing Profiles** page was incorrect\. The correct number of agents for the routing profile was displayed on the **User Management** page\.

### Contact Flows<a name="feb19-flows"></a>
+ Resolved an issue with the contact flow editor when adding intents in Chrome\.
+ Resolved an issue where routing priority and age for queued callbacks were not saved\.
+ Resolved an issue where contact attributes for an outbound whisper flow were not saved\.

### Metrics and Reporting<a name="feb19-metrics"></a>
+ Added **EnqueueTimestamp**, **Duration**, and **DequeueTimestamp** to the contact trace record \(CTR\) for callback contacts\.
+ Resolved an issue where **InitiationTimestamp** for callback contacts did not match the time that the callback was created\.
+ Resolved an issue where users were given an incorrect message when they did not have permissions to edit a report\.

### Contact Control Panel \(CCP\)<a name="feb19-ccp"></a>
+ Resolved an issue where callbacks were not ringing in the CCP\.

## January 2019 Updates<a name="jan19-release-notes"></a>

The following updates were released in January 2019:

**Topics**
+ [Contact Routing](#jan19-contact-routing)
+ [Contact Flows](#jan19-flows)
+ [Metrics and Reporting](#jan19-metrics)

### Contact Routing<a name="jan19-contact-routing"></a>
+ Resolved an issue where in rare cases agent transfers were failing\.

### Contact Flows<a name="jan19-flows"></a>
+ Resolved an issue where agent transfers were failing\.
+ Resolved an issue that resulted in periodic delays in publishing contact flow logs\.

### Metrics and Reporting<a name="jan19-metrics"></a>
+ Resolved an issue in real\-time metrics reports where the page showed the wrong calculation for **Avg queue answer time**\.
+ Resolved an issue where some events were missing from an agent event stream\.

## December 2018 Updates<a name="dec18-release-notes"></a>

The following updates were released in December 2018:

**Topics**
+ [Metrics and Reporting](#dec18-metrics)
+ [Contact Control Panel \(CCP\)](#dec18-ccp)

### Metrics and Reporting<a name="dec18-metrics"></a>
+ Resolved an issue where agent event streams were missing agent snapshots during login and logout events\.
+ Resolved an issue where the contact trace record detail page displayed timestamps using the timezone selected on the search page\.
+ Resolved an issue where the AfterContactWork status was overridden\.
+ Resolved an issue where the timestamps are incorrect if an agent accidentally disconnects while placing a customer on hold\.

### Contact Control Panel \(CCP\)<a name="dec18-ccp"></a>
+ Resolved an intermittent issue with initialization when an agent configuration is corrupted or null\.
+ Resolved an issue where pressing Enter to transfer a call did not work\.

## November 2018 Updates<a name="nov18-release-notes"></a>

The following updates were released in November 2018:

**Topics**
+ [General](#nov18-general)
+ [Contact Flows](#nov18-flows)
+ [Metrics and Reporting](#nov18-metrics)

### General<a name="nov18-general"></a>
+ Resolved an issue with auditing\.
+ Resolved an issue that sometimes resulted in agents being placed in a default state when a contact disconnected when attempting to connect to an agent\.
+ Resolved an issue that sometimes resulted in newly created agents not being able to log in correctly if the log in attempt occurred immediately after user account was created\.

### Contact Flows<a name="nov18-flows"></a>
+ Added the new Loop block, which lets you loop through segments of a contact flow, such as requesting customer information additional times if valid data is not entered\.

### Metrics and Reporting<a name="nov18-metrics"></a>
+ Resolved an issue where callbacks handled were included in the count for incoming contacts in historical reports, but not counted in scheduled reports\. Callbacks handled are no longer included in the count for Incoming contacts handled in historical reports\.
+ Improved performance of report generation for reports with a large number of queues and agents in an instance\.
+ Resolved an issue with how ACW was reported, and backfilled data in customer instances to correct the ACW data for September, October, and November\.

## October 2018 Updates<a name="oct18-release-notes"></a>

The following updates were released in October 2018:

**Topics**
+ [General](#oct18-general)
+ [Metrics and Reporting](#oct18-metrics)
+ [API](#oct18-api)

### General<a name="oct18-general"></a>
+ Resolved an issue that sometimes resulted in stuck media sessions\.

### Metrics and Reporting<a name="oct18-metrics"></a>
+ Resolved an issue that sometimes resulted in agent names not being displayed correctly in historical reports\.
+ Resolved an issue that sometimes resulted in the data related to agent Auxiliary states were incorrectly overwritten\.

### API<a name="oct18-api"></a>
+ Resolved an issue where the `GetCurrentMetrics` operation returned the metric `OLDEST_CONTACT_AGE` was returned in milliseconds instead of seconds\.

## September 2018 Updates<a name="sep18-release-notes"></a>

The following updates were released in September 2018:

**Topics**
+ [General](#sep18-general)
+ [API](#sep18-api)

### General<a name="sep18-general"></a>
+ Improved page loading times for the **User management** page\.
+ Resolved an issue that sometimes caused issues loading the **Queues** page when there were a large number of quick connects associated with a queue\.

### API<a name="sep18-api"></a>
+ Released the [UpdateContactAttributes](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactAttributes.html) operation for the Amazon Connect API\.

## August 2018 Updates<a name="aug18-release-notes"></a>

The following updates were released in August 2018:

**Topics**
+ [General](#aug18-general)
+ [Contact Routing](#aug18-contact-routing)
+ [Metrics and Reporting](#aug18-metrics)

### General<a name="aug18-general"></a>
+ Added a restriction of 64 characters for the password length for the administrator account created during instance creation\.
+ Resolved an issue where the **Hours of operation** page would not load when no days were selected for a saved Hours of operation configuration\.

### Contact Routing<a name="aug18-contact-routing"></a>
+ Increased the timeout for whispers to 2 minutes for outbound and queued callbacks so that agents have longer to prepare for the incoming call\.

### Metrics and Reporting<a name="aug18-metrics"></a>
+ Modified how the value for the Contacts abandoned metric so that calls that transfer to callbacks are not counted as abandoned contacts\.

## July 2018 Updates<a name="july18-release-notes"></a>

The following updates were released in July 2018:

**Topics**
+ [New Features](#july18-features)
+ [General](#july18-general)
+ [Metrics and Reporting](#july18-metrics)
+ [Contact Flows](#july18-contact-flows)

### New Features<a name="july18-features"></a>
+ [Initiate an Outbound Call](using-call-number-block.md)
+ [Add an Amazon Lex Bot](amazon-lex.md)
+ [User Management APIs](https://docs.aws.amazon.com/connect/latest/APIReference/)
+ [Manage Contacts in a Queue](queue-to-queue-transfer.md)

### General<a name="july18-general"></a>
+ Added an error message when attempting to create an admin user during instance creation using “Administrator” as the user name\. The user name Administrator is reserved for internal use, and cannot be used to create a user account in Amazon Connect\.
+ Added support for directory user names that include consecutive dashes\.
+ Added pagination when displaying security profiles in your instance so that more than 25 security profiles can be displayed\.
+ Performance optimizations to reduce latency when using the `StartOutboundVoiceContact` API\.

### Metrics and Reporting<a name="july18-metrics"></a>
+ Resolved an issue in real\-time metrics reports where applied filters were not displayed in the settings page when an additional filter was applied\. The settings page now displays the applied filters correctly\.

### Contact Flows<a name="july18-contact-flows"></a>
+ Added drop\-down menus for contact attributes to make it easier to reference attributes in a contact flows\.

## June 2018 Updates<a name="jun18-release-notes"></a>

The following updates were released in June 2018:

**Topics**
+ [General](#june18-general)
+ [Telephony and Voice](#june18-telephony)
+ [Contact Flows](#june18-contact-flows)
+ [Metrics and Reporting](#june18-metrics)
+ [Contact Control Panel \(CCP\)](#june18-ccp)

### General<a name="june18-general"></a>
+ Changed the font in the UI to Amazon Ember for better readability\.

### Telephony and Voice<a name="june18-telephony"></a>
+ Introduced support for using Amazon Lex bots with Amazon Connect in the US West \(Oregon\) Region\.
+ Fixed a bug that in some cases caused a call to drop when a Loop prompt occurred at the same as a call connecting to an agent\.

### Contact Flows<a name="june18-contact-flows"></a>
+ Renamed the **Set queue** block to **Set working queue**\.
+ Added a **Copy to clipboard** button next to the ARN of a contact flow so you can easily copy the ARN\. Choose **Show additional flow information** under the name of the contact flow in the designer to display the ARN\.
+ Added a new **Call phone number** block, which lets you choose the phone number from your instance to display as the caller ID in an outbound whisper flow\. For more information, see [Initiate an Outbound Call](using-call-number-block.md)\.
+ Released contact attributes for system metrics, including a new **Get metrics** block in contact flows\. For more information, see [How to Use System Metric Attributes](attrib-system-metrics.md)\.

### Metrics and Reporting<a name="june18-metrics"></a>
+ Fixed an issue that caused incorrect rendering of the search field in the filters settings for some historical metrics reports\.
+ Fixed an issue in downloaded reports where the phone number would be blank instead of listing the phone number for calls that were callbacks\.
+ Login/Logout reports now support 20,000 rows per report generation, up from 10,000\.

### Contact Control Panel \(CCP\)<a name="june18-ccp"></a>
+ Added a mute button to the CCP and a mute function to the Streams API so agents can mute and unmute active calls\.

## April and May 2018 Updates<a name="may18-release-notes"></a>

The following updates were released in April and May 2018:

**Topics**
+ [General](#may18-general)
+ [Telephony and Voice](#may18-telephony)
+ [Contact Flows](#may18-contact-flows)
+ [Metrics and Reporting](#may18-metrics)
+ [Contact Control Panel \(CCP\)](#may18-ccp)

### General<a name="may18-general"></a>
+ New [Amazon Polly voices](https://docs.aws.amazon.com/polly/latest/dg/voicelist.html) are now automatically made available in Amazon Connect as soon as they are launched\. You can use new voices, such as Matthew and Léa, in your contact flows\.
+ Updated password enforcement for Amazon Connect user accounts to match requirements for the Amazon Connect admin account created during instance creation\.
+ Resolved an issue that sometimes resulted in the email addresses not being saved when updating an existing user account\.

### Telephony and Voice<a name="may18-telephony"></a>
+ Service optimizations to reduce latency and improve caller ID for Japanese telephony\.
+ Customers can now place calls to Jersey and Guernsey in the Channel Islands\.
+ Added support for keypad numeric input to an Amazon Lex bots when used in an Amazon Connect contact flow\. For more information, see [Amazon Connect Now Supports Keypad Input with an Amazon Lex Chatbot](http://aws.amazon.com/about-aws/whats-new/2018/05/amazon-connect-now-supports-keypad-input-with-an-amazon-lex-chat/)\.
+ Reduced latency for the contact control panel, improving the agent user experience\.

### Contact Flows<a name="may18-contact-flows"></a>
+ Resolved an issue with publishing a contact flow in the case where an **AWS Lambda function block** is used in a contact flow, and the input type for a parameter was changed from **Send attribute** with a **System** attribute is changed to **Send text**\. These contact flows now publish successfully\.
+ Agent and customer whispers are now maintained with queued callbacks\.
+ Attributes now correctly persist with queue callbacks\.
+ Contact attributes are now maintained when using a **Loop prompt** block in a queue flow\.

### Metrics and Reporting<a name="may18-metrics"></a>
+ Data for scheduled reports is now delayed by 15 minutes to allow for most recent data to be incorporated in to reports\. Previously, in some cases, report data for the final 15 minute period during the scheduled report interval did not get included in scheduled reports\. This applies to all report types\.
+ In metric calculations, the time that an incoming call rings is attributed to idle time if the agent is in idle state before an incoming call\.
+ The metric **Agent on contact time** now includes time that an agent spent in an auxiliary busy state\.
+ Published new documentation about metrics\.

### Contact Control Panel \(CCP\)<a name="may18-ccp"></a>
+ Added a **Save** button to the settings menu for the CCP when an agent is using a desk phone\. The **Save** button saves the deskphone configuration between sessions\.
+ Agent username is now available as part of agent configuration data in the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md)\.
+ Contact attributes are now available when using the streams\.js \(Streams API\) for screenpops after queued callbacks\.
+ Fixed issue where for some auto\-accept calls, the agent continued to hear ringing after accepting and joining the call\.