# Release notes for Amazon Connect<a name="amazon-connect-release-notes"></a>

To help you keep track of the ongoing updates and improvements to Amazon Connect, we publish release notices that describe recent changes\.

## April 2023 Updates<a name="apr23-release-notes"></a>

### Customer Profiles displays case information in the agent workspace<a name="agent-workspace-case-info-apr23"></a>

Using Amazon Connect Customer Profiles inside the agent workspace, agents can see cases from third\-party case management solutions and Amazon Connect Cases inside a particular customer profile\. For more information, see [Use Customer Profiles](customer-profiles.md) and [Access Customer Profiles in the agent workspace](customer-profile-access.md)\.

### Added Cross\-channel concurrency<a name="routing-profiles-apr23"></a>

You can configure an agent's routing profile to receive contacts from multiple channels at the same time\. For example, while an agent is on a voice contact, they can be offered contacts from any other channels enabled in the routing profile, such as chats and tasks\.

For more information, see [Create a routing profile](routing-profiles.md)\. Also see the [CrossChannelBehavior](https://docs.aws.amazon.com/connect/latest/APIReference/API_CrossChannelBehavior.html) API\. 

### Set Voice ID block supports fraud watchlist ID<a name="set-voiceid-apr23"></a>

Updated the [Set Voice ID block](https://docs.aws.amazon.com/connect/latest/adminguide/set-voice-id.html) so it supports fraud watchlist ID for fraud detection\. 

### Search, sort, and filter published agent schedules<a name="search-sort-filter-agent-schedules-apr23"></a>

Schedulers can quickly search, sort, and filter agent schedules from within the published schedule calendar\. For more information, see [How supervisors view published schedules](scheduling-view-schedule-supervisors.md)\.

## March 2023 Updates<a name="mar23-release-notes"></a>

### Added Wisdom support for Microsoft SharePoint Online<a name="wisdom-mar23"></a>

You can choose Microsoft SharePoint Online as knowledge base for Wisdom articles\. For more information, see [Enable Amazon Connect Wisdom for your instance](enable-wisdom.md)\. Also see the [AppIntegrationsConfiguration](https://docs.aws.amazon.com/wisdom/latest/APIReference/API_AppIntegrationsConfiguration.html) API in the *Amazon Connect Wisdom API Reference*\. 

### Create step\-by\-step guides for your agents<a name="step-by-step-guides-mar23"></a>

Inside the out\-of\-the\-box Amazon Connect agent workspace, you can create workflows that walk agents through custom UI pages that suggest what to do at a given moment during a customer interaction\. You can create guides that help agents identify customer issues and recommend subsequent actions, as well as surface screen\-pops and forms for submitting transactions and disposition codes\. For more information, see [Agent Workspace guided experience](step-by-step-guided-experiences.md)\.

### Added support for nested JSON in Invoke AWS Lambda function flow block<a name="nest-json-labmda-flow-block-mar23"></a>

The Invoke AWS Lambda function flow block supports JSON responses\. For more information, see [Flow block: Invoke AWS Lambda function](invoke-lambda-function-block.md)\.

### Added Show View flow block<a name="show-view-block-mar23"></a>

This block is used to configure UI based workflows that you can surface to users in front end applications\. For more information, see [Flow block: Show view](show-view-block.md)\.

### Added staff level shift profile<a name="wfm-mar23"></a>

You can assign a shift profile to individual agents\. This is useful to do when, for example, you have part\-time agents who are in the same staffing group as your full\-time agents, but they require their own shift profile\. For more information, see the **Associate to shift profile** option described in [Create staff rules for scheduling](scheduling-create-staff-rules.md)\.

### Added support for multiple fraudster watchlists<a name="fraudster-mar23"></a>

Every domain has a default watchlist where all existing fraudsters are placed by default\. You can create and manage custom watchlists to be evaluated against for known fraudster detection\. For more information, see [Known fraudster detection](https://docs.aws.amazon.com/connect/latest/adminguide/voice-id.html#fraud-detection), and see new actions in the [Amazon Connect Voice ID API Reference](https://docs.aws.amazon.com/voiceid/latest/APIReference/Welcome.html)\.

### Search and sort schedules in the Schedule Manager<a name="scheduling-manager-search-sort-mar23"></a>

Schedulers can quickly search for schedule names using partial keywords or sort the schedule list based on start date, end date, creation date, or updated date\. For more information, see [Search and sort a schedule](scheduling-publish-schedule.md#scheduling-manager-search-sort)\.

### Added the ability to configure multiple IAM roles that can be assigned to a single user when using SAML 2\.0<a name="multi-role-saml-mar23"></a>

You can configure multiple IAM roles that can be assigned to a single user when using SAML 2\.0 which enables you to support user access from multiple identity providers simultaneously\. For example, if you are migrating identity providers, you can configure multiple IAM roles associated to a single user and that user will be able to access Amazon Connect from either provider\. To learn more about configuring IAM roles for SAML 2\.0 in Amazon Connect, see the [Configure SAML with IAM for Amazon Connect](configure-saml.md) documentation\.

### Added panel template for interactive chat messages<a name="interactive-messages-mar23"></a>

With a panel template, you can present customers with up to 10 choices under one question in a chat message\. For more information, see [Add interactive messages to chat](interactive-messages.md)\.

### Added `GetMetricDataV2` API<a name="getmetricdatav2-mar23"></a>

Added the [GetMetricDataV2](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricDataV2.html) API to the *Amazon Connect API Reference Guide*\. This API enables you to programmatically access trailing 14 days of historical agent and contact metrics data\. It extends the capabilities of the [GetMetricData](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetMetricData.html) API, provides new [historical metrics](https://docs.aws.amazon.com/connect/latest/adminguide/historical-metrics-definitions.html) \(for example, the number of [contacts disconnected](https://docs.aws.amazon.com/connect/latest/adminguide/historical-metrics-definitions.html#contact-disconnected-historical), and the number of [callback attempts](https://docs.aws.amazon.com/connect/latest/adminguide/historical-metrics-definitions.html#callback-attempts-historical)\), and provides the ability to filter metrics with more granularity\. 

## February 2023 Updates<a name="feb23-release-notes"></a>

### Added new attribute type `ENHANCED_CONTACT_MONITORING` to Describe, List and Update Instance Attribute APIs<a name="enhanced-monitoring-feb23"></a>

This release updates the APIs: DescribeInstanceAttribute, ListInstanceAttributes, and UpdateInstanceAttribute\. You can use it to programmatically enable/disable enhanced contact monitoring using attribute type `ENHANCED_CONTACT_MONITORING` on the specified Amazon Connect instance\. For more information, see [DescribeInstanceAttribute](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeInstanceAttribute.html), [ListInstanceAttributes](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListInstanceAttributes.html), and [UpdateInstanceAttribute](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateInstanceAttribute.html)\. 

### Added the `DeleteDomain` API for Cases<a name="cases-feb23"></a>

For more information, see the [DeleteDomain](https://docs.aws.amazon.com/cases/latest/APIReference/API_DeleteDomain.html) API in the *Amazon Connect Cases API Reference Guide*\.

### Added `RelatedContactId` to `StartTaskContact` API<a name="tasks-feb23"></a>

You can link together an unlimited number of task contacts using the `RelatedContactID` parameter supported in the `StartTaskContact` API\. For more information, see [Linked tasks](https://docs.aws.amazon.com/connect/latest/adminguide/tasks.html#linked-tasks) and the [StartTaskContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html) API in the *Amazon Connect API Reference Guide*\.

### Amazon Connect Cases integrates with AWS PrivateLink<a name="cases-privatelink-feb23"></a>

For more information, see [Creating an interface VPC endpoint for Amazon Connect](vpc-interface-endpoints.md#vpc-endpoint-create)\.

### Added support for more granular access controls \(using resource tags\) to view real\-time metrics for agents, queues, and routing profiles<a name="tag-based-access-control-real-time-metrics-feb23"></a>

You can enable more granular access controls for real\-time metrics by configuring resource tags and access control tags within security profiles in the Amazon Connect admin website\. For more information, see [Real\-time tag\-based access control](https://docs.aws.amazon.com/connect/latest/adminguide/rtm-tag-based-access-control.html) and [Tag based access control in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tag-based-access-control.html)\.

### Added support to provide more granular permissions to metrics reports, including new permissions for real\-time metrics, historical metrics, and agent activity audit<a name="rtm-granular-permissions-metric-reports-feb23"></a>

You can configure more granular permissions to metrics and reports from within security profiles in the Amazon Connect admin website\. For more information, see [Permissions required to view real\-time metrics reports](https://docs.aws.amazon.com/connect/latest/adminguide/rtm-permissions.html) and [Agent activity audit permissions](https://docs.aws.amazon.com/connect/latest/adminguide/agent-activity-audit-permissions.html)\.

### Added support to provide visibility into an agent’s next activity<a name="agent-activity-visability-feb23"></a>

You can view an agent’s next activity in the real\-time metrics agent table in the Amazon Connect real\-time metrics UI and by using the public API\. For more information, see the [NextStatus API reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_UserData.html#connect-Type-UserData-NextStatus)\.

### Apply S3 Object Lock for the call recordings bucket<a name="objectlock-feb23"></a>

You can use Amazon S3 Object Lock in combination with your call recording bucket to help prevent call recordings from being deleted or overwritten for a fixed amount of time, or indefinitely\. For more information, see [How to set up S3 Object Lock for immutable call recordings](https://docs.aws.amazon.com/connect/latest/adminguide/set-up-recordings.html#s3-object-lock-call-recordings)\.

### CloudFormation templates for instance management<a name="cfn-feb23"></a>

You can use CloudFormation templates to manage Amazon Connect instances for associating Amazon Lex and Lex V2 bots, Lambda functions, security keys, and approved origins—along with the rest of your AWS infrastructure—in a secure, efficient, and repeatable way\. For more information, see [Amazon Connect resource type reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Connect.html) in the *AWS CloudFormation User Guide*\.

## January 2023 Updates<a name="jan23-release-notes"></a>

### Added long lasting, persistent chat experiences<a name="chat-jan23"></a>

Amazon Connect makes it easier for you to deliver long lasting, persistent chat experiences for your customers\. Persistent chats enable customers to resume previous conversations with the context, metadata, and transcripts carried over, eliminating the need for customers to repeat themselves and allowing agents to provide personalized service with access to the entire conversation history\. To set up persistent chat experiences, provide a previous contact ID when calling the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API to create a new chat contact\.

For more information, see [Enable persistent chat](https://docs.aws.amazon.com/connect/latest/adminguide/chat-persistence.html)\. Also see changes to [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) in the *Amazon Connect API Reference Guide*, and see the new `RelatedContactId` parameter in the [GetTranscript](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_GetTranscript.html) API in the *Amazon Connect Participant Service API Reference Guide*\.

## December 2022 Updates<a name="dec22-release-notes"></a>

### Added message receipts feature for chat messages<a name="messages-dec-2022"></a>

The message receipts feature allows customers to receive *Message delivered* and *Read* receipts after they send a chat message\. For more information, see [Enable message Delivered and Read receipts in your chat user interface](https://docs.aws.amazon.com/connect/latest/adminguide/message-receipts.html)\. Also see the [SendEvent](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_SendEvent.html) action, and the [Item](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_Item.html), [MessageMetadata](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_MessageMetadata.html), and [Receipt](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_Receipt.html) data types in the *Amazon Connect Participant Service API Reference Guide*\. 

### Updates to GetCurrentMetricData and GetCurrentUserData<a name="getcurrentmetricdata-dec-2022"></a>

For the [GetCurrentMetricData](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentMetricData.html) API, added support for routing profile filter, sort criteria, and grouping by routing profiles\. For the [GetCurrentUserData](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentUserData.html) API, added support for routing profiles, user hierarchy groups, and agents as filters, and next status and agent status name\. For both APIs, added ApproximateTotalCount\.

### Added chat timeouts for chat participants<a name="chat-timeouts-dec-2022"></a>

When a chat conversation between an agent and a customer has been inactive \(no messages sent\) for a certain amount of time, you may want to consider a chat participant to be idle, and you may even want to automatically disconnect an agent from the chat\. To set up chat timeout timers, see [Set up chat timeouts for chat participants](https://docs.aws.amazon.com/connect/latest/adminguide/setup-chat-timeouts.html)\. 

### Microsoft Edge Chromium support<a name="edge-dec-2022"></a>

Amazon Connect now supports Microsoft Edge Chromium\. For more information about supported browsers, see [Browsers supported by Amazon Connect\.](https://docs.aws.amazon.com/connect/latest/adminguide/connect-supported-browsers.html) 

### Amazon Connect supports JSON as a content type for chat messages<a name="jsoncontenttype-dec-2022"></a>

By supporting JSON as a content type, Amazon Connect provides you with a way to pass additional information over chat to provide rich personalized experiences\. For example, rendering updates to a custom UI, customer\-built interactive messages, language translation capabilities, and passing customer metadata to a third party bot\. For more information, see [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) in the *Amazon Connect API Reference Guide*, and [SendMessage](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_SendMessage.html) in the *Amazon Connect Participant Service API Reference Guide*\. 

### Added topic on Amazon Connect availability by Region<a name="regions-dec-2022"></a>

For more information, see [Availability of Amazon Connect services by Region](https://docs.aws.amazon.com/connect/latest/adminguide/regions.html)\. 

### Contact Lens granular data redaction<a name="contactlens-redaction-dec-2022"></a>

When you set up Contact Lens sensitive data redaction, you can choose which entities you want to redact, and how you want the redaction to appear in the transcript\. For more information, see [Enable redaction of sensitive data](https://docs.aws.amazon.com/connect/latest/adminguide/enable-analytics.html#enable-redaction)\. 

### Additional Contact Lens language support and Region availability<a name="contactlens-regions-dec-2022"></a>

Contact Lens now [supports the following languages](https://docs.aws.amazon.com/connect/latest/adminguide/supported-languages.html#supported-languages-contact-lens): English \- New Zealand, English \- South Africa\. It is also [available in the following Regions](https://docs.aws.amazon.com/connect/latest/adminguide/enable-analytics.html#regions-contactlens): Africa \(Cape Town\), Asia Pacific \(Seoul\), Asia Pacific \(Singapore\)\. 

### Released Barge to allow contact center managers to join ongoing calls<a name="monitor-barge-dec-2022"></a>

Barge allows managers to join and participate in an ongoing customer service call between a contact center agent and customer\. After joining the call, a manager can speak with the customer, add participants, and even choose to remove an agent if needed\. For more information, see [Barge live conversations](https://docs.aws.amazon.com/connect/latest/adminguide/monitor-barge.html)\.

### Added user hierarchy to bulk user upload<a name="bulk-userupload-dec-2022"></a>

You can assign the user hierarchy in the \.csv file when you add users in bulk\. For more information, see [Add users in bulk](https://docs.aws.amazon.com/connect/latest/adminguide/user-management.html)\.

### Granular access controls using resource tags for users, security profiles, routing profiles, and queues<a name="tag-based-access-control-dec-2022"></a>

You can now enable more granular access controls for security profiles, users, routing profiles, and queues by configuring resource tags within the Amazon Connect console\. You can add resource tags to filter and organize these resources logically, and configure access control tags within security profiles to enforce granular permissions\. For more information, see [Tagging resources in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tagging.html) and [Tag based access controls in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tag-based-access-control.html)\.

### Bulk user import now includes agent hierarchy and tags<a name="bulk-user-import-tags-dec-2022"></a>

Amazon Connect now allows you to configure hierarchies and resource tags for users in bulk\. You can now assign agent hierarchies and resource tags to each agent using the CSV bulk upload template which is available on the user management page\. For more information, see [Tagging resources in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/user-management.html)\.

### Released Rules Function language<a name="rules-language-dec-2022"></a>

The Rules Function language is a JSON\-based representation of a series of rule conditions\. Use it to programmatically add conditions to rules\. For more information, see [Amazon Connect Rules Function language](https://docs.aws.amazon.com/connect/latest/APIReference/connect-rules-language.html) in the *Amazon Connect API Reference Guide*\.

### GA for Rules APIs<a name="rules-api-ga-dec-2022"></a>

Released a set of Rules APIs that enable you to programmatically create and manage rules\. For more information, see [Rules actions](https://docs.aws.amazon.com/connect/latest/APIReference/rules-api.html) in the *Amazon Connect API Reference*\.

### Search contacts by agent's first or last name is available in AWS GovCloud<a name="search-contacts-dec-2022"></a>

## November 2022 Updates<a name="nov22-release-notes"></a>

### Create step\-by\-step guides for your agents<a name="step-by-step-guides-nov-2022"></a>

Inside the out\-of\-the\-box Connect agent workspace, you can now create workflows that walk agents through custom UI pages that suggest what to do at a given moment during a customer interaction\. You can create guides that help agents identify customer issues and recommend subsequent actions, as well as surface screen\-pops and forms for submitting transactions and disposition codes\. For more information, see [Agent Workspace guided experience](https://docs.aws.amazon.com/connect/latest/adminguide/step-by-step-guided-experiences.html)\.

### GA for Forecasting, capacity planning, and scheduling<a name="forecasting-nov-2022"></a>

Amazon Connect provides a set of services powered by machine learning that help you optimize your contact center by offering the following:
+ Forecasting\. Analyze and predict contact volume based on historical data\.
+ Scheduling\. Generate agent schedules for day\-to\-day workloads that are flexible, and meet business and compliance requirements\.
+ Capacity planning\. Predict how many agents your contact center will require\. 

For more information, see [Forecasting, capacity planning, and scheduling](https://docs.aws.amazon.com/connect/latest/adminguide/forecasting-capacity-planning-scheduling.html)\. 

### Released Contact Lens evaluation forms for preview<a name="contactlens-chat-nov-2022"></a>

You can create evaluation forms, and then make them available to managers to review conversations alongside contact details, recordings, transcripts, and summaries, without the need to switch applications\. Conversational analytics automatically pre\-populates evaluation scores for criteria like script adherence, sensitive data collection, and customer greetings\. For more information, see [Evaluate performance \(Preview\)](https://docs.aws.amazon.com/connect/latest/adminguide/evaluations.html)\. 

### Released Contact Lens conversational analytics capabilities for Amazon Connect chat<a name="contactlens-chat-nov-2022"></a>

Contact Lens for Amazon Connect provides conversational analytics capabilities for Amazon Connect chat, extending the machine learning powered analytics to better assess chat contacts\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/analyze-conversations.html)\. 

### Added configurable Lex timeouts in chat<a name="lextimeouts-nov-2022"></a>

You can configure how long to wait for a response from a customer in a chatbot conversation before the session expires\. For more information, see *Configurable time\-outs for chat input* in the [Get customer input](https://docs.aws.amazon.com/connect/latest/adminguide/get-customer-input.html) topic\. 

### Create rules that send email notifications<a name="rules-nov-2022"></a>

You can create Contact Lens rules that send email notifications to people in your organization\. For more information, see [Create Contact Lens rules that send email notifications](https://docs.aws.amazon.com/connect/latest/adminguide/contact-lens-rules-email.html)\. 

### Added MonitorContact API<a name="monitor-contact-api-nov-2022"></a>

Added a new API for programmatically initiating monitoring of ongoing contacts\. For more information, see [MonitorContact API](https://docs.aws.amazon.com/connect/latest/APIReference/API_MonitorContact.html)\. 

### Manage saved reports \(admin\)<a name="managed-saved-reports-nov-2022"></a>

You can view and delete all saved reports in your instance, including reports that were not created by you or that are not currently published\. For more information, see [Manage saved reports \(admin\)](https://docs.aws.amazon.com/connect/latest/adminguide/manage-saved-reports-admin.html)\. 

### Search for profiles using multiple search keys<a name="multi-key-search-nov-2022"></a>

In addition to searching for profiles with a single search key \(i\.e\., a key\-values\(s\) pair\), the SearchProfiles API has been enhanced to support searching for profiles using multiple keys and logical operators\. This new functionality allows you to use between 1 and 5 search keys with `AND` or `OR` logic to find profiles with attributes that match the search criteria\. For more information, see the [SearchProfiles API reference](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html)\. 

### Delete quick connects using the Amazon Connect console<a name="quickconnects-nov-2022"></a>

In addition to deleting quick connects programmatically, you can now delete them using the Amazon Connect console\. For more information, see [Delete quick connects](https://docs.aws.amazon.com/connect/latest/adminguide/quick-connects-delete.html)\. 

### Added DismissUserContact API<a name="dismissusercontact-api-nov-2022"></a>

Added a new API for programmatically clearing the notifications agents receive after they have missed or rejected a contact, making them eligible to be routed new contacts\. This API can also be used to clear similar notifications when an agent encounters an error with accepting the contact or is handling After Contact Work\. For more information, see the [DismissUserContact API reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_DismissUserContact.html)\.

## October 2022 Updates<a name="oct22-release-notes"></a>

### Add secondary email address and mobile number to user accounts<a name="user-management-oct-2022"></a>

For more information, see [Add users to Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/user-management.html)\. 

### Emojis for chat messages<a name="emoji-oct-2022"></a>

Added support for emojis for your customer's chat experience\. Agents and customers can now send emojis when composing a chat message, enabling them to visually convey sentiment or emphasis during a chat conversation\. For more information, see [ Enable text formatting for your customer's chat experience](https://docs.aws.amazon.com/connect/latest/adminguide/enable-text-formatting-chat.html)\.

### Released support for Enhanced 911 \(E911\)<a name="e911-oct-2022"></a>

Enhanced 911 \(E911\) enables location information to be sent to 911 dispatch when a 911 call is placed\. In addition to connecting a user with 911 emergency services, customers in the United States can build E911 capabilities to automatically provide the caller's address information to 911 dispatchers\. For more information, see [Set up US emergency calling in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/setup-us-emergency-calling.html)\. 

### GA for Amazon Connect Global Resiliency<a name="global-resiliency-oct-2022"></a>

Released Amazon Connect Global Resiliency for General Availability\. Global Resiliency enables you to provide customer service anywhere in the world with the highest reliability, performance, and efficiency, while meeting international regulatory requirements\. For more information, see [Set up Amazon Connect Global Resiliency](https://docs.aws.amazon.com/connect/latest/adminguide/setup-connect-global-resiliency.html)\. 

### Added Ctrl\+Shift\+F to search flow block titles and metadata<a name="flow-designer-oct-2022"></a>

Press **Ctrl\+Shift\+F** to display a search box in the flow designer, and then search the block titles and metadata\. To hide the search box, go to **Settings**, **Toolbar**, and set the toggle\.

The following GIF shows how to use the search box to find flow blocks that have **attributes** in their title\. It also shows how to display or hide the search box using the toggle\. 

![\[Use the Search box in the flow designer to find flow blocks that have attributes in their title. To hide the Search box from your toolbar, turn the toggle to Off.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/Search-Designer.gif)

### Released Amazon Connect Cases for General Availability<a name="cases-oct-2022"></a>

Amazon Connect Cases allows your agents to quickly track and manage customer issues that require multiple interactions, follow\-up tasks, and teams in your contact center\. For more information, see [Amazon Connect Cases](https://docs.aws.amazon.com/connect/latest/adminguide/cases.html) and [Amazon Connect Cases API Reference](https://docs.aws.amazon.com/cases/latest/APIReference/Welcome.html)\.

## September 2022 Updates<a name="sept22-release-notes"></a>

### Searching for a contact? Choose from a list of categories<a name="contact-search-sep-2022"></a>

When you search a contact and filter results by Contact Lens categories, you can pick from a list of categories, rather than manually typing the name of a category\.

### Updated flow designer<a name="flow-designer-sept-2022"></a>

We've released a number of improvements to the flow designer experience to make building and editing flows easier\.
+ Updated look and feel of block dock, blocks, and flow designer canvas\.  
![\[Access the new flow designer experience by clicking Try now in the banner at the top of the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/NewOptIn.gif)
+ Import / Export uses a standard flow language so you can interchangeably build flows in APIs or in the UI\. 
**Important**  
To copy and paste flows and blocks in the updated flow designer, the flow must be in the new flow language\. To convert a legacy flow into the new format, you have two options:  
Option 1: In the flow designer user interface, opt in to the updated flow designer\. Your legacy flows are automatically converted\.
Option 2: Manually [import](contact-flow-import-export.md) a legacy flow using the updated flow designer\.  
This option is most useful for scenarios where you have stored your flows in JSON offline\. For example, for configuration control, you may have flow configurations in an offline data store\. To copy a part of that flow and paste it into the updated flow designer, you need to import it into the updated flow designer\. The importing process converts it to the new flow language\. After that, you can copy and paste within the updated flow designer\. If you want to keep using your offline data store as a source of truth, update the flow with the new format\.
+ You can use **Search** to filter blocks in the block dock\.  
![\[.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/FilterBlock.gif)
+ Multi\-line block metadata allows you to click and expand to see block configurations\.  
![\[.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/Metadata.gif)
+ Color\-coded branches and connectors help you distinguish paths\.  
![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ColorCodedBranches.gif)
+ Improved zooming\.  
![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/Zoom.gif)
+ Flow/module metadata appears at the bottom of the block dock\.  
![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/AdditionalData.gif)
+ New, more intuitive categories \(**Check**, **Analyze**, and **Logic**\) to make it easier to find the blocks you are looking for\.  
![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/NewCategories.gif)
+ Updated user interface in the block **Property** pages\.  
![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/Sidepanel.gif)

### Search for Amazon Connect users by first name, last name, login, and more<a name="search-users-sept-2022"></a>

You can search for Amazon Connect users by first name, last name, user login, agent hierarchy, security profile, and routing profile\. For example, you can search for all Amazon Connect users who have the first name "Jane\."

### Queue dashboard<a name="queue-dashboard-sept-2022"></a>

You can visualize historical queue data by using time series graphs to help identify patterns, trends, and outliers specifically for **Service Level**, **Contacts Queued**, and **Average Handle Time**\. For more information, see [ Visualize: Queue dashboard](https://docs.aws.amazon.com/connect/latest/adminguide/visualize-queue-dashboard.html)\.

## August 2022 Updates<a name="aug22-release-notes"></a>

### Contact search: Apply "Match any" or "Match all" to Contact Lens category searches<a name="contact-lens-aug-2022"></a>

When you search for contacts, and filter by Contact Lens categories, you can apply **Match any** or **Match all** to the search\. For example, you can search contacts with both "category A" and "category B," or with either one of the two categories\.

### Evaluate calls for voice spoofing<a name="voice-spoofing-2022"></a>

Use Voice ID to evaluate calls for voice spoofing\. For more information, see [Voice spoofing detection](https://docs.aws.amazon.com/connect/latest/adminguide/voice-id.html#voice-spoofing-detection) and the [Amazon Connect Voice ID API Reference](https://docs.aws.amazon.com/voiceid/latest/APIReference/Welcome.html)\.

### Added SearchSecurityProfiles API<a name="searchsecurityprofiles-api-aug22"></a>

Added a new API for programmatically searching security profiles\. For more information, see [https://docs.aws.amazon.com/connect/latest/APIReference/API_SearchSecurityProfiles.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_SearchSecurityProfiles.html)\. 

### Released Schedule Adherence \(Preview\)<a name="schedule-adherence-aug22"></a>

Contact center supervisors or managers track schedule adherence to understand when agents are following the schedule that you have created\. This helps ensure you achieve your service level targets, while improving agent productivity and customer satisfaction\. For more information, see [Schedule Adherence](https://docs.aws.amazon.com/connect/latest/adminguide/schedule-adherence.html)\. 

## July 2022 Updates<a name="july22-release-notes"></a>

### Search for contacts by using the agent's first or last name<a name="contact-search-july22"></a>

You can search for contacts using the agent's first or last name\. The filter name is **Agent**\. 

#### Search contacts by agent's first or last name<a name="search-contacts-agent-name"></a>

The following image shows the Agent filter, and the option to choose agents by name\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-agent-name.png)

#### Required permissions to "Agent" search filter<a name="users-view-permissions-contact-search"></a>

To use the **Agent** filter on the **Contact search** page, in your Amazon Connect security profile you must have **Users \- View** permissions, as shown in the following image: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/release-notes-contact-search.png)

When you have **Users \- View** permissions, on the **Contact search** page the **Agent** filter appears, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/release-notes-contact-search3.png)

Without **User \- View** permissions, the **Agent** filter is not visible, and searching contacts by Agent login is not supported, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/release-notes-contact-search2.png)

### Released updates for rich text format rendering<a name="rich-text-formatting-july22"></a>

On the **Contact Search** and **Contact Detail** pages, you can now view chat transcripts that have rich text formatting, such as bold or italic font, bullet points, numbered lists, and hyperlinks\. For more information about getting started with Amazon Connect Chat, see [Set up your customer's chat experience](https://docs.aws.amazon.com/connect/latest/adminguide/enable-chat-in-app.html)\. 

### View call transcript using the CCP or agent application<a name="call-transcript-july22"></a>

Agents can view call unredacted transcripts in the CCP and agent application\. For more information, see [View a call transcript during ACW](https://docs.aws.amazon.com/connect/latest/adminguide/view-call-transcript-ccp.html)\. 

## June 2022 Updates<a name="june22-release-notes"></a>

### Support for Lex intent confidence scores and sentiment analysis<a name="lex-sentiment-scores-june-2022"></a>

You can further personalize the automated self\-service customer experience using Amazon Lex intent confidence scores and sentiment analysis as a branch within your flows\. For more information, see the [Get customer input](https://docs.aws.amazon.com/connect/latest/adminguide/get-customer-input.html) block\. For a list of new contact attributes, see [Amazon Lex contact attributes](https://docs.aws.amazon.com/connect/latest/adminguide/connect-attrib-list.html#attribs-lex-table)\.

### Metrics Updates<a name="metrics-june-2022"></a>

The following updates were released in June 2022\.

**15 minute scheduled reports**

You can now schedule historical metrics to refresh every 15 minutes\. To select 15\-minute schedules, select generate this report **Hourly** every \.25 hours \(this is the top most option in the second dropdown\), for the previous \.25 hours\. The following image shows the values that you need to select\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-15-minute-scheduled-reports.png)

### <a name="new-real-time-metrics-agent-table-by-agent-june2022"></a>

**Filter Real\-Time Metrics Agent Table by Agent**

You can now filter the agent table on the Real\-Time Metrics page by agent\. This filter functions the same as the existing queues, routing profiles, and agent hierarchy filters\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-rtm-agent-filtering.png)

### New contact transferred related metrics<a name="contact-transferred-whats-new"></a>

We are upgrading the existing [Contacts transferred in](historical-metrics-definitions.md#contacts-transferred-in-historical) and [Contacts transferred out](historical-metrics-definitions.md#contacts-transferred-out-historical) historical metrics to have consistent definitions\. We are adding [Contacts transferred in by agent](historical-metrics-definitions.md#contacts-transferred-in-by-agent-historical) and [Contacts transferred out by agent](historical-metrics-definitions.md#contacts-transferred-out-by-agent-historical) for more granular contact transferred related metrics\. 

### Changes to real\-time metrics agent tables<a name="agent-tables-rtm-page"></a>

We are rolling out a new service to maintain the high availability from metrics that you expect from Amazon Connect\. Due to this change, the agent tables are sorted by [agent status](metrics-agent-status.md) instead of by agent login\.

Additionally, the queues and routing profiles table are sorted by agents online instead of by queue or routing profile name\.

### Faster reload times for the Real\-time metrics page<a name="upgrading-rtm-page"></a>

We are upgrading the performance of the **Real\-time metrics** page so reload times are faster\. The page will have the same functionality and user experience as the existing **Real\-time metrics** page\.

### Released Amazon Connect Cases \(Preview\)<a name="cases-preview-june-2022"></a>

Amazon Connect Cases \(Preview\) allows your agents to quickly track and manage customer issues that require multiple interactions, follow\-up tasks, and teams in your contact center\. For more information, see [Amazon Connect Cases \(Preview\)](https://docs.aws.amazon.com/connect/latest/adminguide/cases.html) and [Amazon Connect Cases API Reference \(Preview\)](https://docs.aws.amazon.com/cases/latest/APIReference/Welcome.html)\.

### GA for Amazon Connect outbound campaigns<a name="outbound-communications-june-2022"></a>

Released Amazon Connect outbound campaigns, formerly known as High\-volume outbound communications\. This release includes a set of APIs for creating and managing outbound campaigns\. For more information, see [Enable Amazon Connect outbound campaigns](https://docs.aws.amazon.com/connect/latest/adminguide/outbound-campaigns.html) and [Amazon Connect Outbound Campaigns API Reference](https://docs.aws.amazon.com/connect-outbound/latest/APIReference/Welcome.html.html)\.

### Released GetCurrentUserData API<a name="getcurrentuserdata-june-2022"></a>

Released the [GetCurrentUserData](https://docs.aws.amazon.com/connect/latest/APIReference/API_GetCurrentUserData.html) API\. It enables you to return the real\-time active user data from the specified Amazon Connect instance\.

### Released task templates<a name="task-templates-june-2022"></a>

You can now create custom task templates, making it easy for agents to consistently capture the relevant and required information to create or complete tasks\. For more information, see [Create task templates](https://docs.aws.amazon.com/connect/latest/adminguide/task-templates.html)\. For information about using the API to programmatically create and manage task templates, see the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html) and the [Amazon Connect Resource Type Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Connect.html) in the *AWS CloudFormation User Guide*\.

### New API to transfer contacts<a name="transfercontact-api-june-2022"></a>

Added a new API that you can use to transfer contacts from one agent or queue to another agent or queue at any point after a contact is created\. You can transfer a contact to another queue by providing the flow which orchestrates the contact to the destination queue\. This gives you more control over contact handling and helps you adhere to the service level agreement \(SLA\) guaranteed to your customers\.

For information, see [TransferContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_TransferContact.html) in the *Amazon Connect API Reference*\. 

## May 2022 Updates<a name="may22-release-notes"></a>

### Updated workflow for outbound campaigns<a name="outbound-communications-may-2022"></a>

Updated the workflow for onboarding to outbound campaigns using the Amazon Connect and Amazon Pinpoint user interface\. For more information, see [Enable outbound campaigns](https://docs.aws.amazon.com/connect/latest/adminguide/outbound-campaigns.html)\.

### Voice ID expires speakers<a name="voiceid-may-2022"></a>

For BIPA Compliance, Amazon Connect Voice ID automatically expires speakers that have not been accessed for enrollment, re\-enrollment, or successful authentication for three years\. You can see a speaker's last access time by looking at the `lastAccessedAt` attribute returned by the [DescribeSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeSpeaker.html) and [ListSpeakers](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListSpeakers.html) APIs\. 

For more information, see [What data is stored?](https://docs.aws.amazon.com/connect/latest/adminguide/voice-id.html#voice-id-data-storage) in the [Use real\-time caller authentication with Voice ID](https://docs.aws.amazon.com/connect/latest/adminguide/voice-id.html) topic\.

## April 2022 Updates<a name="april22-release-notes"></a>

### New API to change an agent's current status<a name="api-april28-2022"></a>

Amazon Connect provides an API to programmatically change the current status of an agent\. [Agent statuses](metrics-agent-status.md) are used to determine when an agent is **Available** to be routed contacts in Amazon Connect, versus when they are set to **Offline** or a custom status such as **Lunch** or **Break** and should not be routed contacts\. For more information, see [PutUserStatus](https://docs.aws.amazon.com/connect/latest/APIReference/API_PutUserStatus.html) in the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\.

### New API to search for users by name, agent hierarchies, and tags<a name="api-april22"></a>

Added API to search for user records in your Amazon Connect instance\. This new API provides a programmatic and flexible way to search for users by first name, last name, username, routing profile, security profile, agent hierarchies or tags\. For example, you can now use this API to search for all users tagged with a Department:key value pair\. You can also quickly find a list of all users assigned to a specific security profile, routing profile, or agent hierarchy\. For more information, see the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\. 

### New APIs to claim and configure phone numbers<a name="api-april22"></a>

Added new APIs to claim new phone numbers and configure them programmatically\. Using these APIs, you can programmatically search for and claim available phone numbers, associate phone numbers to flows, or release phone numbers that are no longer needed\. Additionally, the phone number APIs come with support for AWS CloudFormation\. For more information, see the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html) and the [Amazon Connect Resource Type Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Connect.html) in the *AWS CloudFormation User Guide*\. 

### Telephony: Multi\-party calls<a name="telephony-april22"></a>

You can enable Amazon Connect to allow up to six parties on a call: the agent, the caller, and four more participants\. \(By default, Amazon Connect allows agents to have up to three parties on a call: the agent, and caller, and another participant\.\) For more information, see [Update instance settings](https://docs.aws.amazon.com/connect/latest/adminguide/update-instance-settings.html)\. For more information, see [Host multi\-party calls](multi-party-calls.md)\.

For information about new functionality on the existing Connection and Contact API in Amazon Connect Streams, see the [Amazon Connect Streams Readme](https://github.com/amazon-connect/amazon-connect-streams/blob/master/README.md)\. 

The following sections describes how managing multi\-party calls differs from managing three\-party calls\.

**Topics**
+ [New behavior with multi\-party calls](#telelphony-new-behavior)
+ [Comparison: Three\-party and multi\-party calls](#comparison-multi-party)

#### New behavior with multi\-party calls<a name="telelphony-new-behavior"></a>
+ All agents see all of the connections in a call\.
+ All agents have exactly the same capabilities as any other agent on the call\. This takes into affect the moment an agent accepts the invitation to join the call\.
+ Before a warm transfer is complete, an agent can start talking to the caller as well as disconnect any other agent on the call\.

#### Comparison: Three\-party and multi\-party calls<a name="comparison-multi-party"></a>

The following table summarizes the differences between the agent's experience using the Contact Control Panel \(CCP\) for three\-party calls and multi\-party calls\.
+ Primary agent: the first agent on the call\.
+ Secondary agent: any agent other than the first agent on the call\.


| Three\-party calls | Multi\-party calls | 
| --- | --- | 
|  Agent can control hold, resume, and disconnect only the parties they added\.  |  All agents are have the same call control capabilities\.  | 
|  Agent can add one other participant to an existing call, for a total of three participants \(the agent, the caller, and another participant\)\.  |  Any agent on the call can add additional participants, as long as the total number of participants on the call, including themselves, does not exceed six\.  | 
|  Agent can put only the party they added on hold\.  |  Any agent on the call can put any party on hold\.  | 
|  When a primary agent places a secondary agent on hold, the secondary agent can't take themselves off hold\.  |  Any agent on the call can take themselves off hold\.  | 
|  Secondary agent can talk to the primary agent during hold\.  |  Secondary agents cannot talk to each other until they are taken off hold\.   | 
|  Primary agent can only mute themselves\. Secondary agent can only mute themselves\.  |  Any agent on the call can mute any other participant on the call\.  | 
|  When an agent disconnects \(leaves or is disconnected\), call control continues to be available to the remaining agent\(s\) on the call\.  |  When an agent disconnects, control of the call is transferred to the remaining agents\.   | 
|  Only the primary agent can disconnect a party on the call\. The secondary agent can disconnect the caller only if the primary agent has disconnected\.  |  All agents have the capability to disconnect any other party\.  | 
|  The primary agent can see two connections \(caller and another party\), while a secondary agent sees only the transfer connection\.  |  All agents can see all connections\.  | 
|  An agent only sees **internal transfer** for another agent on the call\.  |  An agent sees the quick connect ID for other agents, instead of just **internal transfer**\.  | 
|  Not applicable\.  |  When an party is being dialed, an agent on a multi\-party call cannot add another party until the prior dial operation is completed \(party added or call leg terminated\)\.  | 

### Play prompts from an Amazon S3 bucket<a name="playprompt-april22"></a>

Added the ability to source prompts from an Amazon S3 bucket\. You can store as many voice prompts as needed in Amazon S3 and access them in real time by using contact attributes in the following contact blocks that play prompts: [Get customer input](get-customer-input.md), [Loop prompts](loop-prompts.md), [Play prompt](play.md), and [Store customer input](store-customer-input.md)\.

For more information, see the [Play prompt](play.md) block\. For information about the policy required for Amazon Connect to access the Amazon S3 bucket, see [Set up prompts to play from an S3 bucket](setup-prompts-s3.md)\.

### CloudTrail support for queues and routing profiles<a name="cloudtrail-april22"></a>

Amazon Connect records all changes made to users, routing profiles, and queues as events in AWS CloudTrail\. For example, you can identify who took which action, what resources were acted upon, and when an event occurred\. For more information, see [Logging Amazon Connect API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

## March 2022 Updates<a name="march22-release-notes"></a>

### Rich messaging for chat<a name="chat-march22"></a>

Added support for rich messaging for your customer's chat experience\. Agents and customers can use bold, italics, bulleted lists, numbered lists, hyperlinks, and attachments\. For more information, see [Enable text formatting for your customer's chat experience](https://docs.aws.amazon.com/connect/latest/adminguide/enable-text-formatting-chat.html)\.

### Customer Profiles: Object type mapping user interface<a name="customerprofiles-march22"></a>

Added a user interface for creating object type mapping by using the Amazon Connect admin console\. For more information, see [Create an object type mapping](https://docs.aws.amazon.com/connect/latest/adminguide/create-object-type-mapping.html)\.

## February 2022 Updates<a name="feb22-release-notes"></a>

### Added bulk ingestion of data for Customer Profiles<a name="customerprofiles-feb22"></a>

Added support for the bulk ingestion of data for Customer Profiles\. For more information, see *Bulk ingestion of data* in the [Set up integration for Salesforce, ServiceNow, Marketo, or Zendesk](https://docs.aws.amazon.com/connect/latest/adminguide/integrate-customer-profiles-appflow.html) topic\.

### New CloudWatch metrics for chat<a name="chat-feb22"></a>

Added the following Amazon CloudWatch metrics for chat: **ConcurrentActiveChats**, **ConcurrentActiveChatsPercentage**, **ChatBreachingActiveChatQuota**, and **SuccessfulChatsPerInterval**\. For more information, see [Monitoring your instance using CloudWatch](monitoring-cloudwatch.md)\. 

## January 2022 Updates<a name="jan22-release-notes"></a>

### Configure maximum chat duration up to 7 days<a name="chat-jan22"></a>

You can configure the maximum chat duration to last up to 7 days\. For more information, see the `ChatDurationInMinutes` parameter in the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API\. 

### Add custom vocabularies to Contact Lens<a name="contact-lens-jan22"></a>

Improve the accuracy of speech recognition for product names, brand names, and domain\-specific terminology, by expanding and tailoring the vocabulary of the speech\-to\-text engine in Contact Lens\. For more information, see [Add custom vocabularies](add-custom-vocabulary.md)\. 

## Earlier Updates<a name="release-notes-earlier-updates"></a>

### December 2021 Updates<a name="dec21-release-notes"></a>

#### Chat widget supports browser notifications<a name="chatwidget-dec21"></a>

The chat widget supports browser notifications for desktop devices\. For more information, see [Browser notifications](browser-notifications-chat.md)\.

#### Ingest data into Customer Profiles from Segment and Shopify<a name="cp-dec21"></a>

For more information, see [Set up integration for Segment](https://docs.aws.amazon.com/connect/latest/adminguide/integrate-customer-profiles-segment.html) and [Set up integration for Shopify](https://docs.aws.amazon.com/connect/latest/adminguide/integrate-customer-profiles-shopify.html)\.

### November 2021 Updates<a name="nov21-release-notes"></a>

#### Released unified agent application<a name="agent-app-nov21"></a>

Amazon Connect released the unified agent application to improve the agent experience and customer interactions\. For more information, see [Agent training guide](https://docs.aws.amazon.com/connect/latest/adminguide/agent-user-guide.html)\.

#### Released call summarization<a name="call-summarization-nov21"></a>

Contact Lens for Amazon Connect provides the option for you to view a transcript summary\. The summary shows only those lines where Contact Lens has identified an issue, outcome, or action item in the transcript\. For more information, see [View call summary](https://docs.aws.amazon.com/connect/latest/adminguide/contact-lens-call-summarization.html)\.

#### Released Identity Resolution to consolidate similar profiles<a name="identity-resolution-nov21"></a>

Amazon Connect Customer Profiles offers Identity Resolution, a feature that is designed to automatically detect similar customer profiles by comparing name, email address, phone number, date of birth, and address\. For example, two or more profiles with spelling mistakes, such as "John Doe" and "Jhn Doe," can be detected as belonging to the same customer "John Doe" using clustering and matching machine learning \(ML\) algorithms\. Once a group of profiles are detected to be similar, admins can configure how profiles should be merged together by setting up consolidation rules by using the [Amazon Connect admin console](https://docs.aws.amazon.com/connect/latest/adminguide/use-identity-resolution.html) or [Amazon Connect Customer Profiles APIs](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/Welcome.html)\.

#### Amazon Connect Customer Profiles stores contact history at no charge<a name="cp-no-charge-nov21"></a>

Amazon Connect Customer Profiles now provides contact history and customer information together in unified customer profiles at no charge, helping contact center managers personalize the contact center experience\. In new instances, Customer Profiles is enabled by default\. For more information, see [Step 4: Data Storage](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instances.html#get-started-data-storage) in the *Create an Amazon Connect instance* topic\.

#### Added modular flows to help you create common functions<a name="flow-modules-nov21"></a>

Flow modules are reusable sections of a flow\. You can create them to extract repeatable logic across your flows, and create common functions\. For more information, see [Flow modules for reusable functions](https://docs.aws.amazon.com/connect/latest/adminguide/contact-flow-modules.html)\.

#### New APIs to archive/unarchive and delete contact flows<a name="flow-apis-nov21"></a>

Added new APIs that provide a programmatic and flexible way to manage your library of flows at scale\. For example, flows used only during certain times of the year can be archived when not in use and then unarchived when needed\. You can now also delete a flow so it is no longer available for use\. For more information, see the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\.

#### Search contacts by custom contact attributes<a name="search-contact-attributes-nov21"></a>

Added support for searching contacts by custom contact attributes \(also called user\-defined attributes\)\. For more information, see [Search by custom contact attributes](https://docs.aws.amazon.com/connect/latest/adminguide/search-custom-attributes)\.

#### Added Customer profiles block<a name="cp-block-nov21"></a>

Added the [Customer profiles](https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-block) block\. It enables you to retrieve, create, and update a customer profile\.

#### Released Contact APIs<a name="contact-apis-nov21"></a>

Added APIs so you can get and update contact details programmatically\. For example, you can describe contact details such as queue information, chat attachments, task references, and update contact information such as task name\. For more information, see [DescribeContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeContact.html), [UpdateContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContact.html), and [ListReferences](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListReferences.html) in the *Amazon Connect API Reference*\.

#### Released scheduled tasks<a name="tasks-nov21"></a>

Added the ability to schedule tasks up to six days in the future to follow\-up on customer issues when promised\. You can also update the scheduled date and time using the [UpdateContactSchedule](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactSchedule.html) API\. For more information, see the [Create task](https://docs.aws.amazon.com/connect/latest/adminguide/create-task-block.html) block and the [Create a task](https://docs.aws.amazon.com/connect/latest/adminguide/create-task.html) topic in the *Agent training guide*\. 

#### Released security profiles APIs<a name="security-profiles-nov21"></a>

Added APIs so you can create and manage security profiles programmatically\. Security profiles help you manage who can access the Amazon Connect dashboard and Contact Control Panel \(CCP\), and who can perform specific tasks\. For more information, see the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\. 

#### Changes to real\-time metrics agent tables<a name="agent-tables-nov21"></a>

We are rolling out a new service to maintain the high availability from metrics that you expect from Amazon Connect\. Due to this change, the agent tables are sorted by [agent status](metrics-agent-status.md) instead of by agent login\.

Additionally, the queues and routing profiles table are sorted by agents online instead of by queue or routing profile name\.

#### Added new metrics<a name="metrics-nov21"></a>

Added following new historical metrics: **Contacts transferred in by agent** and **Contacts transferred out by agent**\. Added new real\-time metrics: T**ransferred in by agent** and **Transferred out by agent**\. For more information, see [Historical metrics definitions](https://docs.aws.amazon.com/connect/latest/adminguide/historical-metrics-definitions.html) and [Real\-time metrics definitions](https://docs.aws.amazon.com/connect/latest/adminguide/real-time-metrics-definitions.html)\.

### October 2021 Updates<a name="oct21-release-notes"></a>

#### Released real\-time chat message streaming<a name="chat-oct21"></a>

You can subscribe to a real\-time stream of chat messages\. For more information, see [Enable real\-time chat message streaming](https://docs.aws.amazon.com/connect/latest/adminguide/chat-message-streaming.html)\.

#### Released `HoursOfOperation` APIs for General Availability<a name="apis-oct21"></a>

Released the Amazon Connect `HoursOfOperation` APIs for general availability \(GA\)\. Also launched AWS CloudFormation support for Users, User Hierarchies, and Hours of Operation\. For more information, see the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html) and the [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Connect.html )\.

### September 2021 Updates<a name="sept21-release-notes"></a>

#### Released Amazon Connect Wisdom General Availability<a name="wisdom-sept21"></a>

For more information, see [Deliver information to agents using Amazon Connect Wisdom](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-wisdom.html) and the [Amazon Connect Wisdom API Reference](https://docs.aws.amazon.com/wisdom/latest/APIReference/Welcome.html)\. 

#### Amazon Connect Voice ID \- General Availability<a name="voiceid-sept21"></a>

For more information, see [Use real\-time caller authentication with Voice ID](https://docs.aws.amazon.com/connect/latest/adminguide/voice-id.html) and the [Amazon Connect Voice ID API Reference](https://docs.aws.amazon.com/voiceid/latest/APIReference/Welcome.html)\. 

#### Preview release of Amazon Connect outbound campaigns<a name="outbound-sept21"></a>

Added content for the preview release of outbound campaigns\. By using Amazon Pinpoint Journeys and Amazon Connect, you can now create outbound campaigns for voice, SMS, and email\. For more information, see [Enable outbound campaigns](https://docs.aws.amazon.com/connect/latest/adminguide/outbound-campaigns.html)\. 

#### New Amazon AppIntegrations Service APIs<a name="appintegrations-apis"></a>

New DataIntegration APIs for the Amazon AppIntegrations Service: `CreateDataIntegration`, `DeleteDataIntegration`, `GetDataIntegration`, `ListDataIntegrationAssociations`, `ListDataIntegrations`, `UpdateDataIntegration`\. 

For more information, see [Amazon AppIntegrations Service API Reference](https://docs.aws.amazon.com/appintegrations/latest/APIReference/Welcome.html)\.

#### Display name and contact attributes in chat<a name="chat-sept21"></a>

You can now personalize the chat experience, as you can specify the name of your customer that interacts using the chat user interface\. You can also securely pass the contact attributes to capture information about the contact which can be used in the flow to further personalize the experience\. For more information, see [Pass the customer display name when a chat initializes](https://docs.aws.amazon.com/connect/latest/adminguide/pass-display-name-chat.html) and [Pass contact attributes when a chat initializes](https://docs.aws.amazon.com/connect/latest/adminguide/pass-contact-attributes-chat.html)\. 

#### Preview of agent application<a name="customerprofiles-sept21"></a>

Launched an updated UI for the agent application preview that combines Customer Profiles and the Contact Control Panel \(CCP\)\. For more information, see [Access Customer Profiles in the agent application](https://docs.aws.amazon.com/connect/latest/adminguide/customer-profile-access.html)\. 

#### Added Create task block<a name="contactblocks-sept21"></a>

Added the **Create task** block\. It creates a new task, sets the tasks attributes, and initiates a flow to start the task\. For more information, see [Flow block: Create task](https://docs.aws.amazon.com/connect/latest/adminguide/create-task-block.html)\. 

### August 2021 Updates<a name="august21-release-notes"></a>

#### Improved user interface for Amazon Connect console<a name="adminconsole-august21"></a>

Released a redesigned and improved user interface for the Amazon Connect console, making it easier and faster to manage Amazon Connect instances\. For more information, see [Create an Amazon Connect instance](amazon-connect-instances.md)\. 

#### APIs for Hours of Operation and Agent Status \(Preview\)<a name="apis-august21"></a>

Released for ungated preview new APIs for managing hours of operation and agent status\. For more information, see [Amazon Connect Service API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\.

#### Contact Lens: Build rules that generate tasks and EventBridge events<a name="contact-lens-august21"></a>

Contact Lens rules now allow you to automatically generate tasks and EventBridge events based on uttered keywords, sentiment scores, customer attributes, and other criteria\. For more information, see [Create rules with Contact Lens](build-rules-for-contact-lens.md)\.

#### Networking: Allow AWS Global Accelerator<a name="august-networking-2021"></a>

When using SAML Sign\-In to your Amazon Connect instance, you now need to add the AWS Global Accelerator domain, **\*\. awsglobalaccelerator\.com**, to your allow list\. For more information, see [Set up your network](ccp-networking.md)\.

### July 2021 Updates<a name="july21-release-notes"></a>

#### "Next status" feature for the CCP<a name="next-status-2021"></a>

In busy contact centers, it can be difficult for agents to take a break or go offline when contacts are being quickly routed to them\. To help agents manage their time, we have released a feature that lets agents pause new contacts being routed to them while they finish their current contacts\. When all their slots are cleared, Amazon Connect automatically sets agents to the next status, such as **Lunch**\.

For details about how agents use this feature, see [Set your "Next status" in the CCP](set-next-status.md)\.

##### Metrics: No changes due to "Next status"<a name="next-status-metrics"></a>

When an agent is in **Next status**, their metrics are the same as when their status is **Available**\.

For example, an agent is handling one contact and chooses **Next status**\. Here's what you'll see in the real\-time metrics report:
+ Agent Activity state = On Contact
+ Agent \- Staffed = 1

**Non\-productive time** \(NPT\) is not incremented when an agent is in **Next status** because the agent is still **Available**\. NPT increments only when the agent actually enters the non\-productive status, such as **Lunch**\.

##### Agent event stream has new NextAgentStatus field<a name="agent-event-stream-next-status"></a>

When an agent sets their status to **Next status**, Amazon Connect populates a new `NextAgentStatus ` field with the next status selected by the agent\. 

At the same time, the `AgentStatus` field continues to display `Available`\. 

The following code snippet shows what the agent event stream looks like when an agent has set their CCP to **Next status: Lunch**\. 

```
"CurrentAgentSnapshot": 
{
    "AgentStatus": {
            "ARN": "example-ARN",
            "Name": "Available",
            "StartTimestamp": "2019-08-13T20:52:30.704Z"
        },
     "NextAgentStatus": {
            "Name": "Lunch",
            "ARN": "example-ARN2",
            "EnqueueTimestamp": "2019-08-13T20:58:00.004Z",
        }
}
```

When an agent has not selected a **Next status**, the field is `null`, as shown in the following snippet:

```
"CurrentAgentSnapshot": {
    "AgentStatus": {
            "ARN": "example-ARN",
            "Name": "Available",
            "StartTimestamp": "2019-08-13T20:52:30.704Z"
        },
     "NextAgentStatus": null
}
```

##### Amazon Connect Streams API and "Next status"<a name="streams-next-status"></a>

The feature has the following effect:
+ If you integrate with Amazon Connect Streams API and your agents interact directly with the native CCP user interface, your agents will start using this new feature immediately\.
+ If you integrate with Amazon Connect Streams API but your agents don't interact directly with the native CCP user interface, your contact center will continue to have the previous behavior when agent\.setState\(\) is called: an agent will not be able to select an NPT or Offline status while connected to at least one contact\. 

  If you are handling state change logic yourself from Amazon Connect Streams, you will need to make additional changes explained in the [Amazon Connect Streams README](https://github.com/amazon-connect/amazon-connect-streams/blob/master/README.md)\. 

#### Contact search: To search contacts by Agent login requires Users \- View permissions in your security profile<a name="contact-search-july21"></a>

To use the **Agent** filter on the **Contact search** page, in your Amazon Connect security profile you must have **Users \- View** permissions, as shown in the following image: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/release-notes-contact-search.png)

When you have **Users \- View** permissions, on the **Contact search** page the **Agent** filter appears, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/release-notes-contact-search1.png)

Without **User \- View** permissions, the **Agent** filter is not visible, and searching contacts by Agent login is not supported, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/release-notes-contact-search2.png)

### June 2021 Updates<a name="june21-release-notes"></a>

#### Apple Messages for Business GA<a name="apple-business-chat-june2021"></a>

Released Apple Messages for Business for general availability \(GA\)\. For more information, see [Enable Apple Messages for Business](apple-business-chat.md)\.

#### Quick connects management API GA<a name="quickconnects-api-june2021"></a>

Released Amazon Connect quick connects management API for general availability \(GA\)\. For more information, see [Amazon Connect Service API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\. The quick connects API also supports AWS CloudFormation\. For more information, see [Amazon Connect Resource Type Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Connect.html) in the AWS CloudFormation User Guide\.

#### Support for Amazon Lex V2 console and APIs<a name="lexv2-june2021"></a>

For more information on using the Amazon Lex V2 console with Amazon Connect, see [Add an Amazon Lex bot](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-lex)\. Added these three APIs: AssociateLexBot, DisassociateLexBot, and ListLexBots\. See the [Amazon Connect Service API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\. 

#### Chat: Increase to chat agent concurrency<a name="chat-june2021"></a>

Chat agents can now handle up to 10 concurrent chat contacts\. For more information, see [Create a routing profile](https://docs.aws.amazon.com/connect/latest/adminguide/routing-profiles)\. 

### May 2021 Updates<a name="may21-release-notes"></a>

#### Added contact events<a name="contact-events-may2021"></a>

Subscribe to a near real\-time stream of contact events \(for example, call is queued\) in your Amazon Connect contact center\. For more information, see [Amazon Connect contact events](contact-events.md)\.

#### Contact search<a name="contact-search-may21"></a>

The following changes were release for Contact search:
+ Download increase: You are able to download 3,000 rows of search results to a CSV file, instead of 1,000 rows\. This increase applies to contacts that occurred after Dec 01, 2020\. 
+ Contact search supports Disconnect Reason as a new filter on the **Contact search** page\. 

  The following image shows how **Disconnect reason** appears in the user interface as a filter\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-disconnectreason.png)

  The following image shows how you can filter by type of disconnect reason\. For a definition of each disconnect reason, see the [ContactTraceRecord](ctr-data-model.md#ctr-ContactTraceRecord) section of the *Contact records data model* topic\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-disconnectreason-choose.png)

  The following image shows how you add **Disconnect reason** as a column to your search results\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-disconnectreason-additionfields.png)

### April 2021 Updates<a name="april21-release-notes"></a>

#### Customer Profiles: Identity resolution<a name="customer-profiles-april2021-"></a>

Added identity resolution APIs to Customer Profiles\. For more information, see the [GetMatches](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetMatches.html) and [MergeProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_MergeProfiles.html) APIs in the Amazon Connect Customer Profiles API reference\.

#### Contact Lens: Use category tags to navigate transcript<a name="contact-lens-april2021-"></a>

For more information, see [Tap or click category tags to navigate through transcript](turn-by-turn-transcript.md#category-navigation)\.

#### Fixes for chat metrics<a name="chat-metrics-april2021"></a>

We released fixes for the following issues identified in chat metrics:
+ Amazon Connect incorrectly reported that chat contacts that were created from disconnect flows were created from transfer flows\.
+ When these fixes, Amazon Connect correctly reflects in the contact records and agent event stream that these chat contacts were created from disconnect flows\. 

There is no impact to voice or task contacts\. 

Chat contacts created through disconnect flows no longer increment the following metrics: 
+ [Contact flow time](historical-metrics-definitions.md#contact-flow-time-historical) 
+ [Contacts incoming](historical-metrics-definitions.md#contacts-incoming-historical)
+ [Contacts handled incoming](historical-metrics-definitions.md#contacts-handled-incoming-historical)
+ [Contacts transferred in](historical-metrics-definitions.md#contacts-transferred-in-historical)

In addition, note the following fixes for contact records and the agent event stream for chat contacts:
+ Contact records: There was an issue in the Attributes section of a chat contact record where the initiation method is **API** for both disconnect and transfer contacts\. With this fix, the initiation method correctly reflects **Disconnect** and **Transfer**, respectively\. 
+ Agent event stream: Chat contacts created from disconnect flows now have **Disconnect** as the initiation method\. 

### March 2021 Updates<a name="march21-release-notes"></a>

#### Amazon Connect is now available in the Canada \(Central\) Region<a name="new-domain"></a>

Amazon Connect is now available in the Canada \(Central\) Region\. You can claim toll\-free and local telephone numbers from Canadian telephony suppliers\. For a list of countries were the Canada \(Central\) Region is supported, see [Region requirements for phone numbers](https://docs.aws.amazon.com/connect/latest/adminguide/phone-number-requirements.html)\. For a list of Contact Lens features available in the Canada \(Central\) Region, see [Availability of Contact Lens features by Region](https://docs.aws.amazon.com/connect/latest/adminguide/enable-analytics.html#regions-contactlens)\. 

#### Domain for new Amazon Connect instances is "my\.connect\.aws"<a name="new-domain"></a>

The domain for the Amazon Connect access URL has changed to **my\.connect\.aws**\.

For example:
+ Current: https://\[*instance name*\]\.**awsapps\.com**/connect/
+ New: https://\[*instance name*\]\.**my\.connect\.aws**/

##### How does this change impact logging in to Amazon Connect?<a name="new-domain-login"></a>

The current access URL continues to work for Amazon Connect instances created before the release of the **my\.connect\.aws** domain\. Any Amazon Connect instances created after the release automatically use the new domain\. 

Also, if you create new Amazon Connect instances after the release of the new domain, you must add new domains to your allow list\. These domains are **in addition** to the ones that are currently required\. 

**Currently required domains added to your allow list:**
+ \{myInstanceName\}\.awsapps\.com/connect/ccp\-v2
+ \{myInstanceName\}\.awsapps\.com/connect/api
+ \*\.cloudfront\.net

**New additional domains to add to your allow list:**
+ \{myInstanceName\}\.my\.connect\.aws/ccp\-v2
+ \{myInstanceName\}\.my\.connect\.aws/api
+ \*\.static\.connect\.aws

For more information, see [Set up your network](ccp-networking.md)\.

##### Schedule for domain change<a name="new-domain-schedule"></a>

The change has been rolled out to all Regions\.

#### March 2021<a name="metrics-changes-new-intervals-hmr-march2021"></a>

The following updates were released in March 2021\.

When customizing a historical metrics report, you have the option to select a 15 minutes interval, in addition to the current option of a 30 minutes interval\. 

The 15 minutes interval works the same as the 30 minutes interval\. For example, you can query up to three days of data at a time, for the past 35 days\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-15-minute-interval.png)

#### Chat: Add a chat user interface your website<a name="march21-chat"></a>

Added a chat widget that you can customize and secure so it can only be launched from your widget\. For more information, see [Set up your customer's chat experience](enable-chat-in-app.md)\.

Provided an open source example\. For more information, see [Download and customize our open source example](download-chat-example.md)\.

#### Amazon Connect Endpoint Test Utility<a name="march21-troubleshoot"></a>

To help you validate connectivity to Amazon Connect, or troubleshoot when your agents are experiencing problems with the Contact Control Panel \(CCP\), we've added the Amazon Connect Endpoint Test Utility\. For more information, see [Use the Endpoint Test Utility](check-connectivity-tool.md)\.

### February 2021 Updates<a name="february21-release-notes"></a>

#### Contact Lens: Availability of real\-time analytics<a name="february21-contact-lens"></a>

Content Lens real\-time analytics is available in Europe \(London\), Europe \(Frankfurt\), and Asia \(Tokyo\)\. For more information, see [Contact Lens features by Region](regions.md#regions-contactlens)\.

#### Ingest data into Customer Profiles using Amazon S3<a name="february21-customer-profiles"></a>

Added the ability to create and ingest data from Amazon S3\. For more information, see [Create and ingest customer data into Customer Profiles by using Amazon S3](customer-profiles-object-type-mappings.md)\.

#### Disconnect reason in contact record stream<a name="february21-metrics"></a>

The Amazon Connect contact records stream now includes **DisconnectReason** for voice calls and tasks\. **DisconnectReason** indicates whether an agent or customer disconnected the call, or whether a telecom or network issue caused a call to disconnect\. You can also determine whether a task was completed by an agent or an automatic flow, or it expired\. For more information, see [ContactTraceRecord](ctr-data-model.md#ctr-ContactTraceRecord)\.

#### Custom service levels<a name="february21-metrics"></a>

Added the ability to create custom service levels\. For details, see [New metric groupings and categories](#metrics-changes-custom-service-levels)\.

#### Metrics updates<a name="metrics-changes-february-2021"></a>

The following updates were released in February 2021\. 

##### New metric groupings and categories<a name="metrics-changes-custom-service-levels"></a>

With the release of [custom service level metrics](#custom-service-levels), we also made the following changes:
+ On the **Table settings** pages, pre\-set and [custom service level metrics](#custom-service-levels) are in a new group called **Contact Service Levels**\.
+ Historical metrics on the **Table settings** page are grouped into categories\. 
+ The order of metric columns on historical metrics reports changed to match the order of the metrics on the **Table settings** page\.

Following is more information about these changes\.

##### Real\-time metrics: New Contact Service Level category<a name="custom-service-levels-rtm"></a>

A new category of metrics appears on the **Table settings** page: **Contact Service Level**\.

The following image shows this new category on the **Table settings** page, in an expandable group\. Choose the arrow next to the group to view and select the metrics you want to add to your report\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-csl-groups.png)

Use the **Contact Service Level** category to choose pre\-set service level metrics, and to create custom service level metrics\.

The following image shows the user interface for creating custom service level metrics\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-create-csl.png)

##### Historical metrics: New categories for metrics<a name="hmr-new-categories"></a>

To make it easier to find the historical metrics you want to add to a report, metrics on the **Table settings** page are grouped into the following categories:
+ Agents
+ Contacts Abandoned
+ Contact Service Level: This group contains preset and custom service levels\.
+ Contacts Answered
+ Performance

Choose **Add Custom SL** to add custom service levels to your historical metrics report\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-csl-group.png)

##### The order of the metric columns on the historical metrics reports has changed<a name="upcoming-changes-static-columns"></a>

The order of the metric columns on the historical metrics reports matches the updated grouping scheme and order of the metrics on the **Table settings** page\.

This change supports the addition of [custom service level metrics](#custom-service-levels)\. It also allows us to make future improvements for where, for example, control of how a report looks resides on the **Real\-time metrics** page and the **Historical metrics** page, not the **Table settings** page\.

Note how metric columns now appear on reports:
+ When you open the **Real\-time metrics** page, custom service levels appear at the end of the **Performance** group\. 
+ Metrics on existing **Scheduled reports** \(the processed documents that arrive in your Amazon S3 buckets\) are not re\-ordered automatically\. However, if you update an existing report, the metrics are re\-ordered to match the order on the **Table settings** page\.
+ **Service level metrics**:
  + Real\-time metrics reports: Service level metrics are always added to the end of the **Performance** group, in ascending order\. 
  + Historical metrics reports: When you add custom service level metrics, they are added to the end of the report in the order they were created\.

##### Custom service level metrics<a name="custom-service-levels"></a>

You have the ability to add custom service level metrics\. You can also choose from additional durations, such as minutes, hours, or days\.

The maximum duration for a custom service level is 7 days\. That's because in Amazon Connect you can't have a contact that goes longer than 7 days\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/metrics-custom-servicelevels.png)

##### Group by channel in a historical metrics report<a name="metrics-changes-group-by-channel-hmr"></a>

**To group by channel on historical metrics reports**

1. On the navigation menu, choose **Analytics and optimization**, **Historical metrics**, and then choose a report\. 

1. Choose **Settings**\. 

1. On the **Table Settings** page, choose the **Groupings** tab\. Add **Channel**, and choose **Apply**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-grouping-channel.png)

1. The table shows a column for **Channel**, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-channel-label.png)

### January 2021 Updates<a name="january21-release-notes"></a>

#### CCP: Change your audio settings<a name="january21-audio-settings"></a>

Added the ability to change audio settings from the Contact Control Panel \(CCP\)\. This applies to organizations using a customized CCP\. For more information, see [How to use the CCP to change your audio device settings](audio-device-settings.md)\.

#### Queue APIs \(Preview\)<a name="january21-queue-apis"></a>

Added APIs so you can programmatically create and manage queues\. For more information, see [Amazon Connect Service API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\.

#### Amazon AppIntegrations APIs \- GA<a name="january21-appintegrations"></a>

Released Amazon AppIntegrations APIs for general availability \(GA\)\. For more information, see [Amazon AppIntegrations Service API Reference](https://docs.aws.amazon.com/appintegrations/latest/APIReference/Welcome.html)\.

### December 2020 Updates<a name="december20-release-notes"></a>

#### Quick Connect APIs \(Preview\)<a name="december20-quickconnects"></a>

Added APIs so you can programmatically create and manage quick connects\. For more information, see [Amazon Connect Service API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\.

#### Chat: Support for attachments<a name="december20-chat"></a>

Added support for chat attachments\. For more information, see [Enable attachments to share files using chat](enable-attachments.md)\. 

Added the following APIs:
+ [CompleteAttachmentUpload](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CompleteAttachmentUpload.html)
+ [GetAttachment](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_GetAttachment.html)
+ [StartAttachmentUpload](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_StartAttachmentUpload.html)

#### Configurable DTMF timeouts for Lex bots<a name="december20-confdtmf"></a>

For more information, see [Configurable fields for DTMF input](get-customer-input.md#get-customer-input-configurable-dtmf)\. 

#### Tasks<a name="december20-tasks"></a>

Added support for tasks, allowing you to prioritize, assign, track, and even automate tasks across the disparate tools agents use to support customers\. For more information, see [Concepts: Tasks in Amazon Connect](tasks.md)\. 

#### Amazon Connect APIs<a name="december20-connectapis"></a>

Added an Amazon Connect API that provides the ability to create tasks \(`StartTaskContact`\), and a set of preview APIs\. 

**Preview APIs:**
+ `CreateIntegrationAssociation`
+ `DeleteIntegrationAssociation`
+ `ListIntegrationAssociations`
+ `CreateUseCase`
+ `DeleteUseCase`
+ `ListUseCases`

#### Amazon AppIntegrations APIs \(Preview\)<a name="december20-appintegrations"></a>

Added the Amazon AppIntegrations APIs \(Preview\), which enables you to configure and reuse connections to external applications\. For more information, see [Amazon AppIntegrations Service API Reference \(Preview\)](https://docs.aws.amazon.com/appintegrations/latest/APIReference/Welcome.html)\. 

#### Customer Profiles<a name="december20-customerprofiles"></a>

Added Amazon Connect Customer Profiles, enabling agents to create a customer profile for every new contact that comes in\. You can also integrate with external applications that provide customer profile data\. For more information, see [Use Customer Profiles](customer-profiles.md) and the [Amazon Connect Customer Profiles API Reference](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/Welcome.html)\.

#### Real\-time analytics using Contact Lens<a name="december20-contactlens"></a>

Added real\-time analytics for Contact Lens so you can detect and resolve customer issues more proactively while the call is in progress\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md) and the [Amazon Connect Contact Lens API Reference](https://docs.aws.amazon.com/contact-lens/latest/APIReference/Welcome.html)\. 

#### Amazon Connect Voice ID \(Preview\)<a name="december20-voiceid"></a>

Added Amazon Connect Voice ID \(Preview\), which provides for real\-time caller authentication\. For more information, see [Use real\-time caller authentication with Voice ID](voice-id.md)\. 

#### Amazon Connect Wisdom \(Preview\)<a name="december20-wisdom"></a>

Added Amazon Connect Wisdom \(Preview\), which enables agents to search and find content across multiple repositories, such as frequently asked questions \(FAQs\), wikis, articles, and step\-by\-step instructions for handling different customer issues\. For more information, see [Deliver information to agents using Amazon Connect Wisdom](amazon-connect-wisdom.md)\. 

#### Amazon Connect with Apple Messages for Business \(Preview\)<a name="december20-applebusinesschat"></a>

Added support for using Amazon Connect with Apple Messages for Business\. For more information, see [Enable Apple Messages for Business](apple-business-chat.md)\. 

### November 2020 Updates<a name="november20-release-notes"></a>

#### Telephony call metadata attributes<a name="november20-telephony"></a>
+ Added call attributes to improve fraud detection and routing\. For more information, see [Telephony call metadata attributes \(call attributes\)](connect-attrib-list.md#telephony-call-metadata-attributes)\.

#### View historical changes<a name="november20-view-historical-changes"></a>
+ The ability to **View historical changes** on the resource configuration pages is now available for the London Region\. The following differences appear as the changes are rolled out to other Regions\. 
  + Total results: The number feature in the **View historical changes** search page, and page numbers, are replaced with **Previous** and **Next** icons\. 
  + The Username filter requires the entire login name\.

#### Chat<a name="november20-chat"></a>
+ Added interactive message templates\. For more information, see [Add interactive messages to chat](interactive-messages.md)\.

#### APIs<a name="november20-apis"></a>
+ Added APIs so you can programmatically manage your agent hierarchies and agent groups\. For more information, see [Amazon Connect Service API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html)\.
+ Added the following APIs \(in an ungated preview release\):
  + CreateInstance
  + DescribeInstance
  + ListInstances
  + DeleteInstance
  + UpdateInstanceAttribute
  + UpdateInstanceStorageConfig

### October 2020 Updates<a name="october20-release-notes"></a>

The following updates were released in October 2020:

#### Contact flows<a name="october20-contact-flows"></a>
+ Added chat support for whisper flows\. For more information, see [Flow block: Set whisper flow](set-whisper-flow.md)\.

#### Metrics<a name="october20-metrics"></a>
+ Released the following real\-time metrics:
  +  [Avg callback connecting time](real-time-metrics-definitions.md#rtm-avg-callback-connecting-time)
  + [Avg incoming connecting time](real-time-metrics-definitions.md#rtm-avg-incoming-connecting-time)
  +  [Avg outbound connecting time](real-time-metrics-definitions.md#rtm-avg-outbound-connecting-time)

  Released the following historical metrics:
  +  [Agent API connecting time](historical-metrics-definitions.md#htm-agent-api-connecting-time)
  +  [Agent callback connecting time](historical-metrics-definitions.md#htm-agent-callback-connecting-time)
  +  [Agent incoming connecting time](historical-metrics-definitions.md#htm-agent-incoming-connecting-time)
  +  [Agent outbound connecting time](historical-metrics-definitions.md#htm-agent-outbound-connecting-time)
  +  [Average agent API connecting time](historical-metrics-definitions.md#htm-avg-agent-api-connecting-time)
  +  [Average agent callback connecting time](historical-metrics-definitions.md#htm-avg-agent-callback-connecting-time)
  +  [Average agent incoming connecting time](historical-metrics-definitions.md#htm-avg-agent-incoming-connecting-time)
  +  [Average agent outbound connecting time](historical-metrics-definitions.md#htm-avg-agent-outbound-connecting-time)
+ In real\-time metrics reports, added one\-click drill\-downs\. These allow you to drill down into queue and routing profile data in one click\. For more information, see [Use one\-click drill\-downs for Routing profiles and Queues tables](one-click-drill-downs.md)\.
+ Added the **Restrict contact access** permission which enables you to manage a user's access to results on the **Contact search** page based on their agent hierarchy group\. For more information, see [Search for contacts](contact-search.md)\.
+ Added **ContactDetails** and **References** to the contact record\. For more information, see [Contact records data model](ctr-data-model.md)\.

### September 2020 Updates<a name="september20-release-notes"></a>

The following updates were released in September 2020:

#### Service quotas<a name="september20-service-quotas"></a>
+ Updated the service quotas for the following Amazon Connect Participant Service APIs: 
  + [CreateParticipantConnection](amazon-connect-service-limits.md#connect-participant-api-quotas) 
  + [DisconnectParticipant](amazon-connect-service-limits.md#connect-participant-api-quotas) 
  + [GetTranscript](amazon-connect-service-limits.md#connect-participant-api-quotas) 

#### Contact flows<a name="september20-contact-flows"></a>
+ Added the Amazon Connect Flow language, a JSON\-based representation of a series of flow actions, and the criteria for moving between them\. For more information, see [Flow language](https://docs.aws.amazon.com/connect/latest/APIReference/flow-language.html)\. 

#### APIs<a name="september20-apis"></a>

Added the following APIs for contact flows:
+ [CreateContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateContactFlow.html)
+ [DescribeContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeContactFlow.html) 
+ [UpdateContactFlowContent](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactFlowContent.html) 
+ [UpdateContactFlowName](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactFlowName.html) 

Added the following API to list prompts:
+ [ListPrompts](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListPrompts.html)

Added the following APIs for routing profiles:
+ [AssociateRoutingProfileQueues](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociateRoutingProfileQueues.html)
+ [CreateRoutingProfile](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateRoutingProfile.html) 
+ [DescribeRoutingProfile](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeRoutingProfile.html)
+ [DisassociateRoutingProfileQueues](https://docs.aws.amazon.com/connect/latest/APIReference/API_DisassociateRoutingProfileQueues.html)
+ [ListRoutingProfileQueues](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListRoutingProfileQueues.html)
+ [UpdateRoutingProfileConcurrency](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateRoutingProfileConcurrency.html)
+ [UpdateRoutingProfileName](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateRoutingProfileName.html)
+ [UpdateRoutingProfileQueues](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateRoutingProfileQueues.html)

### August 2020 Updates<a name="august20-release-notes"></a>

The following updates were released in August 2020:

#### Contact flows<a name="august20-contact-flows"></a>
+ Added the ability to automatically use the best sounding voice available from Amazon Polly for text\-to\-speech\. For more information, see [Amazon Polly best sounding voice](text-to-speech.md#amazon-polly-best-sounding-voice)\. 
+ Added the ability to select, cut, copy, and paste flows\. For more information, see [Copy and paste contact flows](copy-paste-contact-flows.md)\. 

#### Telephony<a name="august20-early-media"></a>
+ Added the ability for all customers to enable/disable media support for outbound phone calls\. For more information, see [Step 3: Set telephony](amazon-connect-instances.md#get-started-telephony) in the [Create an Amazon Connect instance](amazon-connect-instances.md) topic\. 

#### Monitoring<a name="august20-monitoring"></a>
+ Added logging of Amazon Connect Participant Service calls with AWS CloudTrail\. For more information, see [Logging Amazon Connect API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

#### Contact Lens for Amazon Connect<a name="august20-contact-flows"></a>
+ Updated the security profile permissions for the redaction feature\. For more information, see [Security profile permissions for Contact Lens](permissions-for-contact-lens.md)\.

### July 2020 Updates<a name="july20-release-notes"></a>

The following updates were released in July 2020:

#### Contact flows<a name="july20-contact-flows"></a>
+ The **Set voice** block supports speaking styles with neural text\-to\-speech \(TTS\) voices\. For more information, see [Flow block: Set voice](set-voice.md)\.

#### APIs<a name="july20-apis"></a>
+ Added [StartContactRecording](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartContactRecording.html), [StopContactRecording](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContactRecording.html), [SuspendContactRecording](https://docs.aws.amazon.com/connect/latest/APIReference/API_SuspendContactRecording.html), [ResumeContactRecording](https://docs.aws.amazon.com/connect/latest/APIReference/API_ResumeContactRecording.html) to the Amazon Connect Service API\.

#### Contact Lens for Amazon Connect<a name="july20-contact-lens"></a>
+ Updated Contact Lens for Amazon Connect for general availability\. This feature lets you analyze customer\-agent conversations, by using speech transcription, natural language processing, and intelligent search capabilities\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\.

#### Metrics<a name="july20-metrics"></a>
+ Fixed content that was added in June 2020 that said **Agent idle time**,** Agent on contact time**, and **Occupancy** had been deprecated\. That was incorrect\. Rather, they are no longer available for queue groupings only\. For more information, see [What's new in metrics](upcoming-changes.md)\.
+ Corrected how **Occupancy** is calculated\. The correct calculation is: 

  \(Agent on contact \(wall clock time\) / \(Agent on contact \(wall clock time\) \+ Agent idle time\)\)

### June 2020 Updates<a name="june20-release-notes"></a>

The following updates were released in June 2020:

#### June 2020: Changes for omnichannel support<a name="metrics-changes-june-2020"></a>

##### Group by channel<a name="metrics-changes-june-2020-channel"></a>

**To group queues or routing profiles by channel on real\-time metrics reports**

1. On the navigation menu, choose **Analytics and optimization**, **Real\-time metrics**, and then select either **Queues** or **Routing profiles**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-queues-or-routing-profiles.png)

1. Choose **Settings**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-settings.png)

1. On the **Table Settings** page, choose the **Groupings** tab and then select **Queues grouped by channels**\. Or, if you're setting up a **Routing profiles** report, choose **Routing profiles grouped by channels**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-group-by-channel.png)

1. Choose **Apply**\.

1. The table shows a column for **Channel**\.

##### Group by queue in historical metrics reports<a name="metrics-changes-june-2020-queue-grouping"></a>

In the historical metrics report, when you group or filter metrics by **Queue**, the results for the following metrics aren't accurate: 
+ Agent idle time \(not supported in queue grouping as of June, 2020\)
+ Agent on contact time \(not supported in queue grouping as of June, 2020\)
+ Occupancy \(not supported in queue grouping as of June, 2020\)

Because of this, on the **Table Settings** page, **Metrics** tab, these metrics are inactive, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-inactive-metrics.png)

In addition, in the historical metrics report, Amazon Connect displays a hyphen \(\-\) in place of results for these metrics, and the cells are inactive \(gray\)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/hmr-null-metrics.png)

##### Effect of queue grouping on saved and scheduled reports<a name="metrics-changes-june-2020-saved-scheduled-reports"></a>

If the **Queue** grouping or filter is used on the following reports, note these effects: 
+ **Saved reports**\. The columns for these metrics don't appear in the saved reports when *grouped* by Queue\. When the saved report is *filtered* by Queue, however, it shows "\-"\.
+ **Scheduled reports**\. These reports continue to run successfully, but no results are returned for these metrics\. 

##### Agent on contact time \(not supported in queue grouping as of June, 2020\)<a name="metrics-changes-june-2020-agent-on-contact-time"></a>

On historical metrics reports when an agent handles multiple chats concurrently, **Agent on contact time** shows wall clock time: the amount of time spent chatting\. However, there isn't a metric that shows the time an agent spends chatting with each contact\.

In addition, no results are returned when you use the **Queue** grouping or filter with **Agent on contact time**\.

##### Agent idle time \(not supported in queue grouping as of June, 2020<a name="metrics-changes-june-2020-agent-idle-time"></a>

The **Agent idle time** metric divides the idle time into each queue associated with the agent\. When contacts are grouped or filtered by **Queue**, however, Amazon Connect doesn't provide an accurate view into the how the agent is working\. Because of this, Amazon Connect doesn't show **Agent idle time** when you apply the **Queue** grouping or filter to your report\. 

##### Occupancy \(not supported in queue grouping as of June, 2020\)<a name="metrics-changes-june-2020-occupancy"></a>

With the addition of chat, the **Occupancy** metric is now defined as the percentage of time that an agent was active on contacts\. This percentage is calculated as follows:
+ \(Agent on contact \(wall clock time\) / \(Agent on contact \(wall clock time\) \+ Agent idle time\)\) 

Because **Agent idle time** is now inaccurate when contacts are grouped or filtered by **Queues**, the **Occupancy** metric is also inaccurate\. As a result, when contacts are grouped or filtered by Queues, **Occupancy** doesn't appear on the report\.

Occupancy no longer appears on the **Dashboard** page\.

#### Contact Control Panel \(CCP\)<a name="june20-ccp"></a>
+ Released the following improvements:
  + DTMF input is passed to all lines in a three\-way call\. Any party can enter DTMF input\. 
  + Resolved an issue where the DTMF tone degraded when agents interacted with Quick connect and/or Number pad during a session\. 
  + Resolved an issue where quick connects sometimes did not appear on a page, even after an agent refreshed it\.
  + Improved the experience when a manager "listens in" to multiple chat conversations\. Updated the unread message count on the CCP to include messages sent by the customer and those sent by the agent\. Previously, the unread message count only included messages sent by the customer\.
+ Published instructions for upgrading to the latest CCP\. For more information, see [Upgrade to the latest CCP](upgrade-to-latest-ccp.md)\.
+ Published a training video that explains how to use the CCP\. For more information, see [Training video: How to use the CCP](ccp-video-training.md)\.

#### Contact flows<a name="june20-contact-flows"></a>
+ The **Set disconnect flow** block supports voice conversations\. For more information, see [Flow block: Set disconnect flow](set-disconnect-flow.md)\.
+ The **Set Voice** block supports Amazon Polly Neural Text\-to\-Speech \(NTTS\) voices\. For more information, see [Flow block: Set voice](set-voice.md)\.
+ The **Get queue metrics** block can return metrics by channel, for example, by voice or chat\. For more information, see [Flow block: Get queue metrics](get-queue-metrics.md)\.

### May 2020 Update<a name="may20-release-notes"></a>

The following updates were released in May 2020:

#### Contact flows<a name="may20-contact-flows"></a>
+ Added the ability to select multiple blocks at the same time and rearrange them as a group within a flow\. For more information, see [Create an inbound flow](create-contact-flow.md#create-inbound-contact-flow)\.

### April 2020 Update<a name="april20-release-notes"></a>

The following updates were released in April 2020:

#### Telephony<a name="april20-telephony"></a>
+ Added early media support for outbound phone calls\. Enabled by default, an agent hears tones and audio messages played by phone companies—such as busy signals, failure to connect errors, or other informational messages—through their headset or audio device\. For more information, see [Step 3: Set telephony](amazon-connect-instances.md#get-started-telephony) in the [Create an Amazon Connect instance](amazon-connect-instances.md) topic\. 
+ Added the `barge-in-enabled` session attribute to the [Get customer input](get-customer-input.md) block so customers can interrupt Amazon Lex bots with their voice\. 

### March 2020 Update<a name="mar20-release-notes"></a>

The following updates were released in March 2020:

#### Contact flows<a name="mar20-contact-flows"></a>
+ Updated the [Store customer input](store-customer-input.md) block to allow you to specify a custom terminating keypress\.

#### Metrics<a name="mar20-metrics"></a>
+ Announced [June 2020: Changes for omnichannel support](#metrics-changes-june-2020)\.

#### Networking<a name="mar20-networking"></a>
+ Updated softphone requirements in [Set up your network](ccp-networking.md)\.

### February 2020 Update<a name="feb20-release-notes"></a>

The following updates were released in February 2020:

#### Service Quotas<a name="feb20-networking"></a>
+ Adjusted [Amazon Connect service quotas](amazon-connect-service-limits.md) for new accounts\.

#### Contact Flows<a name="feb20-contact-flows"></a>

Updated the following blocks so you can set contact attributes:
+ [Set customer queue flow](set-customer-queue-flow.md)
+ [Set hold flow](set-hold-flow.md) 
+ [Set whisper flow](set-whisper-flow.md) 

### January 2020 Update<a name="jan20-release-notes"></a>

The following updates were released in January 2020:

#### Contact Control Panel \(CCP\)<a name="jan20-ccp"></a>

The following updates were made to the updated Contact Control Panel \(ccp\-v2\):
+ Agents can now transfer a contact by double\-clicking a quick connect\. For more information, see [Transfer calls to a quick connect or external phone number](transfers.md)\.
+ The number pad now retains the previously selected country flag so agents don't need to select it every time\.
+ All strings in the CCP user interface are now localized in available languages\.
+ Resolved an issue where the color of the call status bar incorrectly displayed as green during a conference call when the call was in the Joined state\. It is now blue\.
+ Resolved an issue where the agent’s name was displayed in error messages for missed chats, rather than the customer’s name\.

#### Networking<a name="jan20-networking"></a>
+ Updated [Set up your network](ccp-networking.md) to include requirements for the updated Contact Control Panel \(ccp\-v2\)\.

### December 2019 Update<a name="dec19-release-notes"></a>

The following update was released in December 2019:

#### Monitoring<a name="dec19-monitoring"></a>
+ Added Contact Lens for Amazon Connect for preview\. This feature enables you search conversations for keywords, sentiment scores, and non\-talk time\. For more information, see [Analyze conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\.
+ Added logging of Amazon Connect API calls with AWS CloudTrail\. For more information, see [Logging Amazon Connect API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

### November 2019 Update<a name="nov19-release-notes"></a>

The following updates were released in November 2019:

#### Omnichannel Support<a name="nov19-channel"></a>
+ Added support for chat communications\. For more information, see [Concepts](connect-concepts.md)\. 

#### November 2019<a name="metrics-changes-november-2019"></a>

##### Name changes for "Missed" and "Agent status" and "On call"<a name="metrics-changes-november-2019-names"></a>

The following real\-time metrics were renamed:


| Old name | New name | 
| --- | --- | 
|  Missed  | Agent non\-response  | 
|  Agent status  | Agent activity  | 
|  On call  | On contact  | 

For each metric, existing saved reports automatically start displaying the new name; you don't need to do anything for the new name to appear in your reports\. 

The column order for a saved report containing one of these metrics stays the same\. For example, if you previously saved a report where **Agent status** was the third metric, now when you open that saved report, **Agent activity** is the name for the third metric\.

For **Missed**, only the name of the metric changed; the underlying calculation stayed the same\. We've changing the name of this metric to **Agent non\-response** so it better reflects its definition: 
+ **Agent non\-response** increments whenever a contact is offered to an agent, and the agent doesn't respond to the contact for whatever reason\. 

  For example, the agent could have intentionally let the timer run out, or the agent could have forgotten to grant microphone access in the Contact Control Panel and never heard the ring\. In these situations, Amazon Connect doesn't drop the contact\. Instead, the routing engine will offer it to another available agent, while the customer continues to wait in queue\. This means a single contact could result in multiple **Agent non\-responses** before an agent responds and handles the contact\.

For **On call**, the name change to **On Contact** applies to the Real\-time metrics UI only\. You can continue using `AGENTS_ON_CALL` with the `GetCurrentMetricData` API to retrieve data for this metric\.

##### Label updates for "Agent activity" and "Contact state"<a name="metrics-changes-november-2019-labels"></a>

Labels are the values returned in a report\. For example, in the following image **Available** and **Basic Routing Profile** are labels\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/labels.png)

For **Agent Activity** and **Contact State**, we renamed some of the labels that describe what the agent's current activity is and what's happening with the contact they are currently working on\. This way, the labels in the Real\-Time Metrics report are more consistent with the labels the agent sees in the Contact Control Panel\. They also align with the data returned about these different states in other parts of Amazon Connect\.

When the name of **Agent Status** changed to **Agent Activity**, the following labels changed, too:


| Scenario | Before: Agent Status Labels | After: Agent Activity Labels | Notes | 
| --- | --- | --- | --- | 
|  Agent is logged in but offline  |  Not shown  |  Not shown  |    | 
|  Agent switches to **Available** in the CCP  |  Available  |  Available  |    | 
|  Agent has an incoming call  |  CallIncoming  |  Incoming  |  ContactState = Incoming contact  | 
|  Agent has an incoming callback  |  CallbackIncoming  |  Incoming  |  ContactState = Inbound callback  | 
|  Agent accepted a callback, which is now making an outbound call to the customer  |  Calling  |  On Contact  |  ContactState = Outbound callback  | 
|  Agent makes outbound call \(regardless of what status the agent chose in their CCP\)  |  Calling  |  On Contact  |  ContactState = Outbound contact  | 
|  Agent missed a phone call due to timer expired  |  MissedCallAgent  |  Missed  |    | 
|  Agent is interacting with customer on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |    | 
|  Agent puts customer on hold while on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |    | 
|  After agent hangs up call  |  After call work  |  After contact work  |    | 
|  Agent is on Lunch \(a custom status\)  |  Lunch  |  Lunch  |    | 
|  Supervisor's activity state if they are monitoring some agent  |  Monitoring  |  Monitoring  |    | 
|  Agent's activity state if they are connected to customer while being monitored by a supervisor  |  On call  |  On Contact  |    | 

The following table shows the how the labels changed for **Contact State**\.


| Scenario | Label Name Before | Label Name After | 
| --- | --- | --- | 
|  Agent is logged in but offline  |    |    | 
|  Agent switches to **Available** in the CCP  | \-  | \-  | 
|  Agent has an incoming call  |  \-  |  Incoming contact  | 
|  Agent has an incoming callback  |  \-  |  Inbound callback  | 
|  Agent accepted a callback, which is now making an outbound call to the customer  |  Initial  |  Outbound callback  | 
|  Agent makes outbound call \(regardless of what status the agent chose in their CCP\)  |  Initial  |  Outbound contact  | 
|  Agent missed a phone call due to timer expired  |  Missed call  |  Missed contact  | 
|  Agent is interacting with customer on phone call \(regardless of what status the agent chose in their CCP\)  |  Busy  |  Connected  | 
|  Agent puts customer on hold while on phone call \(regardless of what status the agent chose in their CCP\)  |  OnHold  |  On hold  | 
|  After agent hangs up call  |  After call work  |  After contact work  | 
|  Agent is on Lunch \(a custom status\)  |  \-  |  \-  | 
|  Supervisor's contact state if they are monitoring an agent  |  Monitoring  |  Monitoring  | 

#### Contact Flows<a name="nov19-contact-flows"></a>

Added the following contact flow blocks:
+ [Flow block: Wait](wait.md)
+ [Flow block: Set disconnect flow](set-disconnect-flow.md) 

Updated the following contact flow blocks for chat:
+ [Flow block: Play prompt](play.md)
+ [Flow block: Get customer input](get-customer-input.md)
+ [Flow block: Store customer input](store-customer-input.md)
+ [Flow block: Set recording and analytics behavior](set-recording-behavior.md)

#### User Management<a name="nov19-users"></a>
+ Added that you can use AWS Identity and Access Management \(IAM\) with Amazon Connect\. For more information, see [Identity and access management for Amazon Connect](security-iam.md)\.

#### Live Media Streaming<a name="nov19-lms"></a>
+ Added that you can capture customer audio for the entire interaction with your contact center\. For more information, see [Capture customer audio: live media streaming](customer-voice-streams.md)\.

#### API<a name="nov19-api"></a>
+ Added [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html), [ListTagsForResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListTagsForResource.html), [TagResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_TagResource.html), [UntagResource](https://docs.aws.amazon.com/connect/latest/APIReference/API_UntagResource.html) to the Amazon Connect Service API\.
+ Added the [Amazon Connect Participant Service](https://docs.aws.amazon.com/connect-participant/latest/APIReference/Welcome.html) API\. These APIs are used chat participants, such as agents and customers\.

#### Contact Control Panel \(CCP\)<a name="nov19-CCP"></a>
+ Updated the CCP so it supports chat\. For more information, see [Agent training guide for the CCP and agent workspace](agent-user-guide.md)\. 

### October 2019 Update<a name="oct19-release-notes"></a>

The following update was released in October 2019:

#### Metrics<a name="oct19-metrics"></a>
+ The real time metric **On call** is now incremented whenever an agent is handling a contact who is connected, on hold, in After Contact Work, or the agent is dialog out to a customer\. 

  This metric is available in the Queues tables and Routing Profile tables on the **Real time metrics** page\. It's also returned by the `GetCurrentMetricData` API as `AGENTS_ON_CALL`\. 

### June 2019 Update<a name="June19-release-notes"></a>

The following update was released in June 2019:

#### Contact Flows<a name="june19-flows"></a>
+ Added flow versioning so you can choose between a saved or published version when you roll back\.

### May 2019 Updates<a name="may19-release-notes"></a>

The following updates were released in May 2019:

#### Metrics and Reporting<a name="may19-flows"></a>
+ Improved the error messages you might encounter when creating, editing, or deleting a scheduled report\. 
+ In the Historical metrics report UI, changed **Contacts missed** to **Agent non\-response**\. This metric appears as **Contacts missed** in scheduled reports and exported CSV files\.
+ In the agent event stream, fixed the formatting of the timestamp millisecond so you can better order and analyze the data\. To learn more, see [Amazon Connect agent event streams](agent-event-streams.md)\. 

#### Contact Control Panel<a name="may19-ccp"></a>
+ Resolved an issue where calling a destroy action \(such as `connection.destroy`\) using the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md) resulted in different behavior depending on which leg of the conversation it was called from: the agent or the customer\. Now calling a destroy action results in the same behavior for both: a busy conversation is moved to After Call Work \(ACW\) and a conversation in any other state is cleared\. If you used the native Contact Control Panel instead of the Amazon Connect Streams API, you weren't impacted by this issue\.

### April 2019 Updates<a name="april19-release-notes"></a>

The following updates were released in April 2019:

#### Contact Control Panel<a name="april19-ccp"></a>
+ Resolved an issue where the hold flow didn't run in this case: 
  + The agent missed a call and then set themselves back to Available\.
  + Then they were re\-routed the same call\.
  + The agent put that customer on hold while handling the call\.

  However, taking the customer off hold worked as expected and no other impact occurred\.
+ Resolved an issue where the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md) returned `softphoneAutoAccept = FALSE` even though **Auto\-Accept Call** was enabled for the agent\. 

### March 2019 Update<a name="March19-release-notes"></a>

The following updates were released in March 2019:

#### Metrics and Reporting<a name="march19-flows"></a>
+ Improved the error messages you might encounter when running real\-time metrics reports\. For example, if you manually configure a real\-time metrics report to contain more than 100 queues, we'll display this message: "You've hit the maximum limit of 100 queues\. Please reconfigure your report to contain no more than 100 queues\." To learn more, see [No metrics or too few rows in a queues report?](troubleshoot-rtm.md)

#### Contact Control Panel<a name="march19-ccp"></a>
+ Resolved an issue where, in rare cases, an agent already handling an outbound call could have been incorrectly presented with an additional queued callback, even though they are only allowed to handle one contact at a time\. Since that agent would have been on contact and not idle, the agent wouldn't have been able to accept the queued callback\.

  In these cases, the outbound call was not impacted; the agent wouldn't have noticed any differences in the CCP\. The callback was presented to another agent instead of being dropped\.

### February 2019 Updates<a name="feb19-release-notes"></a>

The following updates were released in February 2019:

**Topics**
+ [Contact Routing](#feb19-contact-routing)
+ [Contact Flows](#feb19-flows)
+ [Metrics and Reporting](#feb19-metrics)
+ [Contact Control Panel \(CCP\)](#feb19-ccp)

#### Contact Routing<a name="feb19-contact-routing"></a>
+ Resolved an issue where in rare cases some contacts were not routed to the agent that was available for the longest time\.
+ Resolved an issue in the user interface where the value displayed for **No\. of agents staffed** for the **Basic Routing Profile** on the **Routing Profiles** page was incorrect\. The correct number of agents for the routing profile was displayed on the **User Management** page\.

#### Contact Flows<a name="feb19-flows"></a>
+ Resolved an issue with the contact flow editor when adding intents in Chrome\.
+ Resolved an issue where routing priority and age for queued callbacks were not saved\.
+ Resolved an issue where contact attributes for an outbound whisper flow were not saved\.

#### Metrics and Reporting<a name="feb19-metrics"></a>
+ Added **EnqueueTimestamp**, **Duration**, and **DequeueTimestamp** to the contact record for callback contacts\.
+ Resolved an issue where **InitiationTimestamp** for callback contacts did not match the time that the callback was created\.
+ Resolved an issue where users were given an incorrect message when they did not have permissions to edit a report\.

#### Contact Control Panel \(CCP\)<a name="feb19-ccp"></a>
+ Resolved an issue where callbacks were not ringing in the CCP\.

### January 2019 Updates<a name="jan19-release-notes"></a>

The following updates were released in January 2019:

**Topics**
+ [Contact Routing](#jan19-contact-routing)
+ [Contact Flows](#jan19-flows)
+ [Metrics and Reporting](#jan19-metrics)

#### Contact Routing<a name="jan19-contact-routing"></a>
+ Resolved an issue where in rare cases agent transfers were failing\.

#### Contact Flows<a name="jan19-flows"></a>
+ Resolved an issue where agent transfers were failing\.
+ Resolved an issue that resulted in periodic delays in publishing flow logs\.

#### Metrics and Reporting<a name="jan19-metrics"></a>
+ Resolved an issue in real\-time metrics reports where the page showed the wrong calculation for **Avg queue answer time**\.
+ Resolved an issue where some events were missing from an agent event stream\.

### December 2018 Updates<a name="dec18-release-notes"></a>

The following updates were released in December 2018:

**Topics**
+ [Metrics and Reporting](#dec18-metrics)
+ [Contact Control Panel \(CCP\)](#dec18-ccp)

#### Metrics and Reporting<a name="dec18-metrics"></a>
+ Resolved an issue where agent event streams were missing agent snapshots during login and logout events\.
+ Resolved an issue where the contact record detail page displayed timestamps using the timezone selected on the search page\.
+ Resolved an issue where the AfterContactWork status was overridden\.
+ Resolved an issue where the timestamps are incorrect if an agent accidentally disconnects while placing a customer on hold\.

#### Contact Control Panel \(CCP\)<a name="dec18-ccp"></a>
+ Resolved an intermittent issue with initialization when an agent configuration is corrupted or null\.
+ Resolved an issue where pressing Enter to transfer a call did not work\.

### November 2018 Updates<a name="nov18-release-notes"></a>

The following updates were released in November 2018:

**Topics**
+ [General](#nov18-general)
+ [Contact Flows](#nov18-flows)
+ [Metrics and Reporting](#nov18-metrics)

#### General<a name="nov18-general"></a>
+ Resolved an issue with auditing\.
+ Resolved an issue that sometimes resulted in agents being placed in a default state when a contact disconnected when attempting to connect to an agent\.
+ Resolved an issue that sometimes resulted in newly created agents not being able to log in correctly if the log in attempt occurred immediately after user account was created\.

#### Contact Flows<a name="nov18-flows"></a>
+ Added the new Loop block, which lets you loop through segments of a flow, such as requesting customer information additional times if valid data is not entered\.

#### Metrics and Reporting<a name="nov18-metrics"></a>
+ Resolved an issue where callbacks handled were included in the count for incoming contacts in historical reports, but not counted in scheduled reports\. Callbacks handled are no longer included in the count for Incoming contacts handled in historical reports\.
+ Improved performance of report generation for reports with a large number of queues and agents in an instance\.
+ Resolved an issue with how ACW was reported, and backfilled data in customer instances to correct the ACW data for September, October, and November\.

### October 2018 Updates<a name="oct18-release-notes"></a>

The following updates were released in October 2018:

**Topics**
+ [General](#oct18-general)
+ [Metrics and Reporting](#oct18-metrics)
+ [API](#oct18-api)

#### General<a name="oct18-general"></a>
+ Resolved an issue that sometimes resulted in stuck media sessions\.

#### Metrics and Reporting<a name="oct18-metrics"></a>
+ Resolved an issue that sometimes resulted in agent names not being displayed correctly in historical reports\.
+ Resolved an issue that sometimes resulted in the data related to agent Auxiliary states were incorrectly overwritten\.

#### API<a name="oct18-api"></a>
+ Resolved an issue where the `GetCurrentMetrics` operation returned the metric `OLDEST_CONTACT_AGE` in milliseconds instead of seconds\.

### September 2018 Updates<a name="sep18-release-notes"></a>

The following updates were released in September 2018:

**Topics**
+ [General](#sep18-general)
+ [API](#sep18-api)

#### General<a name="sep18-general"></a>
+ Improved page loading times for the **User management** page\.
+ Resolved an issue that sometimes caused issues loading the **Queues** page when there were a large number of quick connects associated with a queue\.

#### API<a name="sep18-api"></a>
+ Released the [UpdateContactAttributes](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactAttributes.html) operation for the Amazon Connect API\.

### August 2018 Updates<a name="aug18-release-notes"></a>

The following updates were released in August 2018:

**Topics**
+ [General](#aug18-general)
+ [Contact Routing](#aug18-contact-routing)
+ [Metrics and Reporting](#aug18-metrics)

#### General<a name="aug18-general"></a>
+ Added a restriction of 64 characters for the password length for the administrator account created during instance creation\.
+ Resolved an issue where the **Hours of operation** page would not load when no days were selected for a saved Hours of operation configuration\.

#### Contact Routing<a name="aug18-contact-routing"></a>
+ Increased the timeout for whispers to 2 minutes for outbound and queued callbacks so that agents have longer to prepare for the incoming call\.

#### Metrics and Reporting<a name="aug18-metrics"></a>
+ Modified how the value for the Contacts abandoned metric so that calls that transfer to callbacks are not counted as abandoned contacts\.

### July 2018 Updates<a name="july18-release-notes"></a>

The following updates were released in July 2018:

**Topics**
+ [New Features](#july18-features)
+ [General](#july18-general)
+ [Metrics and Reporting](#july18-metrics)
+ [Contact Flows](#july18-contact-flows)

#### New Features<a name="july18-features"></a>
+ [Outbound caller ID number](queues-callerid.md#using-call-number-block)
+ [Add an Amazon Lex bot to Amazon Connect](amazon-lex.md)
+ [User Management APIs](https://docs.aws.amazon.com/connect/latest/APIReference/)
+ [Manage contacts in a queue](queue-to-queue-transfer.md)

#### General<a name="july18-general"></a>
+ Added an error message when attempting to create an admin user during instance creation using "Administrator" as the user name\. The user name Administrator is reserved for internal use, and cannot be used to create a user account in Amazon Connect\.
+ Added support for directory user names that include consecutive dashes\.
+ Added pagination when displaying security profiles in your instance so that more than 25 security profiles can be displayed\.
+ Performance optimizations to reduce latency when using the `StartOutboundVoiceContact` API\.

#### Metrics and Reporting<a name="july18-metrics"></a>
+ Resolved an issue in real\-time metrics reports where applied filters were not displayed in the settings page when an additional filter was applied\. The settings page now displays the applied filters correctly\.

#### Contact Flows<a name="july18-contact-flows"></a>
+ Added drop\-down menus for contact attributes to make it easier to reference attributes in a contact flows\.

### June 2018 Updates<a name="jun18-release-notes"></a>

The following updates were released in June 2018:

**Topics**
+ [General](#june18-general)
+ [Telephony and Voice](#june18-telephony)
+ [Contact Flows](#june18-contact-flows)
+ [Metrics and Reporting](#june18-metrics)
+ [Contact Control Panel \(CCP\)](#june18-ccp)

#### General<a name="june18-general"></a>
+ Changed the font in the UI to Amazon Ember for better readability\.

#### Telephony and Voice<a name="june18-telephony"></a>
+ Introduced support for using Amazon Lex bots with Amazon Connect in the US West \(Oregon\) Region\.
+ Fixed a bug that in some cases caused a call to drop when a Loop prompt occurred at the same as a call connecting to an agent\.

#### Contact Flows<a name="june18-contact-flows"></a>
+ Renamed the **Set queue** block to **Set working queue**\.
+ Added a **Copy to clipboard** button next to the ARN of a flow so you can easily copy the ARN\. Choose **Show additional flow information** under the name of the flow in the designer to display the ARN\.
+ Added a new **Call phone number** block, which lets you choose the phone number from your instance to display as the caller ID in an outbound whisper flow\. For more information, see [Outbound caller ID number](queues-callerid.md#using-call-number-block)\.
+ Released contact attributes for system metrics, including a new **Get metrics** block in contact flows\. For more information, see [Route based on number of contacts in a queue](attrib-system-metrics.md)\.

#### Metrics and Reporting<a name="june18-metrics"></a>
+ Fixed an issue that caused incorrect rendering of the search field in the filters settings for some historical metrics reports\.
+ Fixed an issue in downloaded reports where the phone number would be blank instead of listing the phone number for calls that were callbacks\.
+ Login/Logout reports now support 20,000 rows per report generation, up from 10,000\.

#### Contact Control Panel \(CCP\)<a name="june18-ccp"></a>
+ Added a mute button to the CCP and a mute function to the Streams API so agents can mute and unmute active calls\.

### April and May 2018 Updates<a name="may18-release-notes"></a>

The following updates were released in April and May 2018:

**Topics**
+ [General](#may18-general)
+ [Telephony and Voice](#may18-telephony)
+ [Contact Flows](#may18-contact-flows)
+ [Metrics and Reporting](#may18-metrics)
+ [Contact Control Panel \(CCP\)](#may18-ccp)

#### General<a name="may18-general"></a>
+ New [Amazon Polly voices](https://docs.aws.amazon.com/polly/latest/dg/voicelist.html) are now automatically made available in Amazon Connect as soon as they are launched\. You can use new voices, such as Matthew and Léa, in your contact flows\.
+ Updated password enforcement for Amazon Connect user accounts to match requirements for the Amazon Connect admin account created during instance creation\.
+ Resolved an issue that sometimes resulted in the email addresses not being saved when updating an existing user account\.

#### Telephony and Voice<a name="may18-telephony"></a>
+ Service optimizations to reduce latency and improve caller ID for Japanese telephony\.
+ Customers can now place calls to Jersey and Guernsey in the Channel Islands\.
+ Added support for keypad numeric input to an Amazon Lex bots when used in an Amazon Connect contact flow\. For more information, see [Amazon Connect Now Supports Keypad Input with an Amazon Lex Chatbot](http://aws.amazon.com/about-aws/whats-new/2018/05/amazon-connect-now-supports-keypad-input-with-an-amazon-lex-chat/)\.
+ Reduced latency for the contact control panel, improving the agent user experience\.

#### Contact Flows<a name="may18-contact-flows"></a>
+ Resolved an issue with publishing a flow in the case where an **AWS Lambda function block** is used in a flow, and the input type for a parameter was changed from **Send attribute** with a **System** attribute is changed to **Send text**\. These flows now publish successfully\.
+ Agent and customer whispers are now maintained with queued callbacks\.
+ Attributes now correctly persist with queue callbacks\.
+ Contact attributes are now maintained when using a **Loop prompt** block in a queue flow\.

#### Metrics and Reporting<a name="may18-metrics"></a>
+ Data for scheduled reports is now delayed by 15 minutes to allow for most recent data to be incorporated in to reports\. Previously, in some cases, report data for the final 15 minute period during the scheduled report interval did not get included in scheduled reports\. This applies to all report types\.
+ In metric calculations, the time that an incoming call rings is attributed to idle time if the agent is in idle state before an incoming call\.
+ The metric **Agent on contact time** now includes time that an agent spent in an auxiliary busy state\.
+ Published new documentation about metrics\.

#### Contact Control Panel \(CCP\)<a name="may18-ccp"></a>
+ Added a **Save** button to the settings menu for the CCP when an agent is using a desk phone\. The **Save** button saves the deskphone configuration between sessions\.
+ Agent username is now available as part of agent configuration data in the [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams/blob/master/Documentation.md)\.
+ Contact attributes are now available when using the streams\.js \(Streams API\) for screenpops after queued callbacks\.
+ Fixed issue where for some auto\-accept calls, the agent continued to hear ringing after accepting and joining the call\.