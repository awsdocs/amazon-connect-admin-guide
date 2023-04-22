# List of security profile permissions<a name="security-profile-list"></a>

The security profile permissions in Amazon Connect allow users access to perform specific tasks in Amazon Connect\.

The following tables list: 
+ **UI name**: The name of the permission as it appears on the **Security profiles** page in Amazon Connect\.
+ **API name**: The name of the permission when it is returned by the [ListSecurityProfilePermissions](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListSecurityProfilePermissions.html) API\.
+ **Use**: The functionality granted by the permission\.

## Routing<a name="routing-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Routing profiles \- Create  |  RoutingPolicies\.Create  | [Create routing profiles](routing-profiles.md)\.  | 
| Routing profiles \- Edit  |  RoutingPolicies\.Edit  | Edit routing profiles\.  | 
| Routing profiles \- View  |  RoutingPolicies\.View  | View routing profiles\.  | 
| Quick connects \- Create  |  TransferDestinations\.Create  | [Create quick connects](quick-connects.md)\.  | 
| Quick connects \- Delete  |  TransferDestinations\.Delete  | [Delete quick connects](quick-connects-delete.md)\.  | 
| Quick connects \- Edit  |  TransferDestinations\.Edit  | Edit quick connects\.  | 
| Quick connects \- View  |  TransferDestinations\.View  | View quick connects\. Agents need this permission so they can view quick connects in the agent application to transfer calls\.  | 
| Hours of operation \- Create  |  HoursOfOperation\.Create  | [Set hours of operation and timezone for a queue](set-hours-operation.md)\.   | 
| HoursOfOperation \- Delete  |  HoursOfOperation\.Delete  | Delete hours of operation and timezone for a queue\.  | 
| HoursOfOperation \- Edit  |  HoursOfOperation\.Edit  | Edit hours of operation and timezone for a queue\.  | 
| HoursOfOperation \- View  |  HoursOfOperation\.View  | View hours of operation and timezone for a queue\.  | 
| Queues \- Create  |  Queues\.Create  | [Create queues](create-queue.md)\.  | 
| Queues \- Edit  |  Queues\.Edit  | Edit information for a queue, such as name, description, and hours of operation\.  | 
| Queues \- Enable / Disable  |  Queues\.EnableAndDisable  | [Enable and disable queues](disable-a-queue.md) to quickly control the flow of contacts to queues temporarily\.  | 
| Queues \- View  |  Queues\.View  | View a list of queues in your Amazon Connect instance\.  | 
| Task templates \- Create  |  TaskTemplates\.Create  | [Create task templates](task-templates.md)\.  | 
| Task templates \- Delete  |  TaskTemplates\.Delete  | Delete task templates\.  | 
| Task templates \- Edit  |  TaskTemplates\.Edit  | Edit task templates\.  | 
| Task templates \- View  |  TaskTemplates\.View  | View task templates\.  | 

## Numbers and flows<a name="numbers-flows-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Prompts \- Create |  Prompts\.Create  | [Create prompts](prompts.md)\.  | 
| Prompts \- Delete |  Prompts\.Delete  | Delete prompts\.  | 
| Prompts \- Edit |  Prompts\.Edit  | Edit prompts\.  | 
| Prompts \- View |  Prompts\.View  | View a list of available prompts\.  | 
| ContactFlows \- Create |  ContactFlows\.Create  | [Create flows](create-contact-flow.md)\.  | 
| ContactFlows \- Delete |  ContactFlows\.Delete  | [Delete flows](create-contact-flow.md#delete-contact-flow)\.  | 
| ContactFlows \- Edit |  ContactFlows\.Edit  | Edit flows\.  | 
| ContactFlows \- Publish |  ContactFlows\.Publish  | Publish flows\.  | 
| ContactFlows \- View |  ContactFlows\.View  | View flows\.  | 
| Contact flow modules \- Create |  ContactFlowModules\.Create  | [Create flow modules for reusable functions](contact-flow-modules.md)\.   | 
| Contact flow modules \- Delete |  ContactFlowModules\.Delete  | Delete flow modules\.  | 
| Contact flow modules \- Edit |  ContactFlowModules\.Edit  | Edit flow modules\.  | 
| Contact flow modules \- Publish |  ContactFlowModules\.Publish  | Publish flow modules\.  | 
| Contact flow modules \- View |  ContactFlowModules\.View  | View flow modules\.  | 
| Phone numbers \- Claim |  PhoneNumbers\.Claim  | [Claim phone numbers](get-connect-number.md)\.  | 
| Phone numbers \- Edit |  PhoneNumbers\.Edit  | Edit phone numbers\. [Attach a claimed or ported phone number to a flow](associate-claimed-ported-phone-number-to-flow.md)\.   | 
| Phone numbers \- Release |  PhoneNumbers\.Release  | [Release phone numbers back to inventory](release-phone-number.md)\.  | 
| Phone numbers \- View |  PhoneNumbers\.View  | View a list of phone numbers that have been claimed or ported to your Amazon Connect instance\.  | 
| Chat test mode \- Enable/Disable |  ChatTestMode  | Access a simulated web page so users can [test the chat experience](chat-testing.md#test-chat)\. Also grants them the permission to view a list of flows, which is exposed through the **Test settings** option\.  | 
| Views |  Views\.View  | Allow access to [Views](view-resources-sg.md)  | 

## Users and permissions<a name="users-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Users \- Create |  Users\.Create  | [Add users to Amazon Connect](user-management.md)\. We recommend you limit who has these permissions\. They pose a risk to your contact center because they can do the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security-profile-list.html) Doing these things would enable someone to lock out those who need to access Amazon Connect, and allow in others who can steal customer data and damage your business\.   | 
| Users \- Delete |  Users\.Delete  | [Delete users from Amazon Connect](delete-users.md)\.  | 
| Users \- Edit |  Users\.Edit  | View and edit user records\. As with **Users \- Create**, limit who has these permissions because they pose a risk to your contact center\.  | 
| Users \- Edit permission |  Users\.EditPermission  | View and edit user records\. As with **Users \- Create**, limit who has these permissions because they pose a risk to your contact center\.  | 
| Users \- View |  Users\.View  | View user records\.  | 
| Agent hierarchy \- Create |  AgentGrouping\.Create  | [Create agent hierarchies](agent-hierarchy.md)\. Add groups, teams, and agents\.  | 
| Agent hierarchy \- Edit |  AgentGrouping\.Edit  | Edit agent hierarchies\.   | 
| Agent hierarchy \- Enable/Disable |  AgentGrouping\.EnableAndDisable  | View or edit agent hierarchy information\.  | 
| Agent hierarchy \- View |  AgentGrouping\.View  | View the agent's hierarchy information in a real\-time metrics report, which can include their location and skill set data\.  | 
| Security profiles \- Create |  SecurityProfiles\.Create  | [Create security profiles](create-security-profile.md)\.  | 
| Security profiles \- Delete |  SecurityProfiles\.Delete  | Delete security profiles\.  | 
| Security profiles \- Edit |  SecurityProfiles\.Edit  | [Update security profiles](update-security-profiles.md)\.  | 
| Security profiles \- View |  SecurityProfiles\.View  | View security profiles\.  | 
| Agent status \- Create |  AgentStates\.Create  | [Create an custom agent status](agent-custom.md)\. The status appears in the Contact Control Panel \(CCP\), such as Break, Lunch, or Training\.   | 
| Agent status \- Edit |  AgentStates\.Edit  | Edit a custom agent status\.  | 
| Agent status \- Enable/Disable |  AgentStates\.EnableAndDisable  | View and edit custom agent states\.  | 
| Agent status \- View |  AgentStates\.View  | [View an agent's status in the real\-time metrics report](rtm-change-agent-activity-state.md) and historical metrics report\. For example, if they are **Available**, **Offline**, or in a custom state\. View their status in the [Agent activity report](agent-activity-audit-report.md)\.  | 

## Contact Control Panel \(CCP\)<a name="ccp-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Access Contact Control Panel |  BasicAgentAccess  | Manages access to the Contact Control Panel \(CCP\)\. Assign this permission to agents as well as managers who need to monitor live conversations\.  | 
| Contact Lens data |  RealtimeContactLens\.View  | Enables users to view real\-time analytics provided by Contact Lens\.  | 
| Make outbound calls |  OutboundCallAccess  | Grants users permissions to make outbound calls\. For more information about setting up outbound calling, see [Set up outbound communications](outbound-communications.md)\.  | 
| Voice ID |  VoiceId\.Access  | Enables controls in the Contact Control Panel so agents can: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security-profile-list.html)  | 
| Restrict task creation |  RestrictTaskCreation\.Access  | Block agents from being able to create tasks\.   | 

## Analytics<a name="analytics-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Access metrics |  AccessMetrics  | [Manage access to real\-time and historical metrics reports](rtm-permissions.md)\.  | 
| Real\-time metrics |  RealTimeMetrics\.Access  | Manage access to the real\-time metrics page\.  | 
| Historical metrics |  HistoricalMetrics\.Access  | Manage access to the historical metrics page\.  | 
| Agent activity audit |  AgentActivityAudit\.Access  | Manage access to the agent activity audit within the historical metrics page\.  | 
| Contact Search |  ContactSearch\.View  | Access the **Contact search** page, which is where users can [search for contacts](contact-search.md) and see results on the **Contact details** page\.  | 
| Search contacts by conversation characteristics |  ContactSearchWithCharacteristics\.Access  | Access to the Contact Lens filters that enable users to search by sentiment scores, non\-talk time, and category\.  | 
| Search contacts by conversation characteristics \- View |  ContactSearchWithCharacteristics\.View  | View the Contact Lens filters that enable users to search by sentiment scores, non\-talk time, and category\.   | 
| Search contacts by keywords |  ContactSearchWithKeywords\.Access  | Search for contacts by keyword\. On the **Contact Search** page, users can access additional filters that allow them to search Contact Lens transcripts by keywords or phrases, such as "thank you for your business\."  | 
| Search contacts by keywords \- View |  ContactSearchWithKeywords\.View  | Search for contacts by keyword\. On the **Contact Search** page, users can access additional filters that allow them to search Contact Lens transcripts by keywords or phrases, such as "thank you for your business\."  | 
| Configure searchable contact attributes \- View |  ConfigureContactAttributes\.View  | Determine what custom attribute data will be searchable \(by people who have the **Contact attributes** permission\)\. It allows them to access the **Searchable custom contact attributes** page\. For more information, see [Search by custom contact attributes](search-custom-attributes.md)\.  | 
| Restrict contact access |  ContactRecording\.Access  | If your organization isn't using Contact Lens for Amazon Connect, use this permission to manage who can listen to recordings, access the corresponding URLs that are generated in S3, and delete recordings\. For more information, see [Assign permissions to review recordings of past conversations](assign-permssions-to-review-recordings.md)\. Checking this box limits a user's access to contacts based on their agent hierarchy\. The user will only have access to contacts handled by agent within their own hierarchy\.  | 
| Restrict contact access |  RestrictContactAccessByHierarchy\.View  | Manage a user's access to results on the **Contact search** page based on their agent hierarchy group\. For more information, see [Manage who can search for contacts and access detailed information](contact-search.md#required-permissions-search-contacts)\.  | 
| Contact attributes |  ContactAttributes\.View  | View contact attributes\. Also controls access to the search filters based on contact attributes\. For more information, see [Search by custom contact attributes](search-custom-attributes.md)\.  | 
| Contact Lens speech analytics \- View |  GraphTrends\.View  | On the **Contact Details** page for a contact, users can view graphs that summarize speech analytics, such as customer sentiment trend, sentiment, and talk time\.  | 
| Contact Lens \- custom vocabularies \- Edit |  ContactLensCustomVocabulary\.Edit  | [Add custom vocabularies](add-custom-vocabulary.md)\.   | 
| Contact Lens \- custom vocabularies \- View |  ContactLensCustomVocabulary\.View  | [Download and view custom vocabularies](add-custom-vocabulary.md#view-custom-vocabulary)\.  | 
| Rules \- Create |  Rules\.Create  | [Create rules](connect-rules.md)\.   | 
| Rules \- Delete |  Rules\.Delete  | Delete rules\.   | 
| Rules \- Edit |  Rules\.Edit  | Edit rules\.   | 
| Rules \- View |  Rules\.View  | View rules\.   | 
| Recorded conversations \(redacted\) |  RedactedData\.View  | On the **Contact details** and **Contact search** pages for a contact, listen to call recording files and view call transcripts in which the sensitive data has been removed\.  | 
| Recorded conversations \(unredacted\) \- View |  ListenCallRecordings  | On the **Contact details** and **Contact search** pages for a contact, view unredacted content that contains sensitive data, such as name and credit card information\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/security-profile-list.html) If you have permissions to both **Recorded conversations \(redacted\)** and **Recorded conversations \(unredacted\)**, note the following behavior:    By default only redacted recordings and transcripts are made available on the **Contact details** and **Contact search** pages\.   When no redacted content exists for the contact, or when redacted content cannot be shown to the user, then unredacted content is displayed on the **Contact details** and **Contact search** pages\.   To access unredacted conversations, remove permissions to **Recorded conversations \(redacted\)**\. This leaves the user with only **Recorded conversations \(unredacted\)** permissions\. You cannot access both the redacted and unredacted version of a conversation at the same time\.   | 
| Recorded conversations \(unredacted\) \- Access |  ListenCallRecordings  | View the Play icon so they can listen to call recordings by using the Amazon Connect user interface\.  | 
| Recorded conversations \(unredacted\) \- Enable download button |  DownloadCallRecordings  | [Download call recordings](download-recordings.md)\. By default, the **Enable download button** permission is granted too so the user can download recordings through the user interface\.  | 
| Recorded conversations \(unredacted\) \- Delete |  DeleteCallRecordings  | Delete call recordings\. By default, the **Enable download button** permission is granted too so the user can delete recordings through the user interface\.  | 
| Login/Logout report \- View |  AgentTimeCard\.View  |  [View Login/Logout reports](login-logout-reports.md)\.   | 
| Manager monitor \- Enable/Disable |  ManagerListenIn  | [Monitor live conversations](monitor-conversations.md) and [listen to recordings of past conversations](review-recorded-conversations.md)\. Be sure to assign managers to the Agent security profile so they can access the Contact Control Panel \(CCP\)\. This enables them to monitor the conversation through the CCP\.  | 
| Saved reports \- View |  MetricsReports\.View  | [View a shared report](view-a-shared-report.md)\.  | 
| Saved reports \- Create |  MetricsReports\.Create MetricsReports\.Share  | [Create and share reports](share-reports.md)\.  | 
| Saved reports \- Edit |  MetricsReports\.Edit  | Edit save reports\.  | 
| Saved reports \- Delete |  MetricsReports\.Delete  | Delete saved reports\.  | 
| Saved reports \- Publish |  MetricsReports\.Publish  | [Publish reports](publish-reports.md)\.  | 
| Saved reports \- Schedule |  MetricsReports\.Schedule MetricsReports\.Publish ReportSchedules\.Create ReportSchedules\.Delete ReportSchedules\.Edit ReportSchedules\.View  | [Schedule a saved report](schedule-historical-metrics-report.md)\. By default, the user gets permission to create, delete, edit, and view a saved report\.  | 
| Evaluation forms \- perform evaluations |   Evaluation\.Create Evaluation\.View  Evaluation\.Edit Evaluation\.Delete  | [Evaluate performance](evaluations.md)\.   | 
| Evaluation forms \- manage form definitions |  EvaluationForms\.Create EvaluationForms\.View  EvaluationForms\.Edit EvaluationForms\.Delete  | [Create and manage evaluation forms](create-evaluation-forms.md)\.   | 
| Voice ID \- attributes and search |  VoiceIdAttributesAndSearch\.View  | Search for and view Voice ID results on the **Contact detail** page\.  | 
| Voice ID \- attributes and search |  VoiceIdAttributesAndSearch\.View  | Search for and view Voice ID results on the **Contact detail** page\.  | 
| Forecasting \- View |  Forecasting\.View  | [Review contact volume and average handle time forecasts](inspect-forecast.md)\.  | 
| Forecasting \- Edit |  Forecasting\.Edit  |  [Create and edit contact volume and average handle time forecasts](create-forecasts.md)\.   | 
| Forecasting \- Publish |  Forecasting\.Publish  | [Publish a forecast](publish-forecast.md)\.  | 
| Capacity planning \- View |  Capacity\.View  | [Review capacity plan output](capacity-planning-review-output.md)\.  | 
| Capacity planning \- Edit |  Capacity\.Edit  | [Create capacity planning scenarios](capacity-planning-create-scenarios.md)\.  | 
| Capacity planning \- Publish |  Capacity\.Publish  | [Publish a capacity plan](publish-capacity-plan.md)\.  | 
| Forecast and schedule interval |  Forecasting\.Edit  | [Set the forecast and schedule interval](set-forecast-scheduling-interval.md)\.  | 

## Historical changes<a name="historical-changes-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| View historical changes |  HistoricalChanges\.View  | On the **User management** page, view historical changes to user records\.  | 

## Customer Profiles<a name="customerprofiles-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Customer profiles \- Create |  CustomerProfiles\.Create  | [Create customer profiles in the agent application](ag-cp-create.md)\.  | 
| Customer profiles \- Edit |  CustomerProfiles\.Edit  | Edit customer profiles in the agent application\.  | 
| Customer profiles \- View |  CustomerProfiles\.View  | Edit customer profiles in the agent application\.  | 

## Scheduling<a name="scheduling-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Schedule manager \- View |  Scheduling\.View  |  [View generated staff schedules in the Schedule manager user experience](scheduling-publish-schedule.md)\.   | 
| Schedule manager \- Edit |  Scheduling\.Edit  | [Create, edit schedule configuration and publish generated staff schedules](scheduling-publish-schedule.md)\.   | 
| Schedule manager \- Publish |  Scheduling\.Publish  | [Publish a schedule](scheduling-publish-schedule.md) by using Schedule Manager\.  | 
| Published schedule calendar |  Scheduling\.View  | [View](scheduling-view-schedule-staff.md) a schedule\.   | 
| Team calendar |  TeamCalendar\.View  | [View published staff schedules in the Published Calendar user experience](scheduling-view-schedule-supervisors.md)\.   | 
| Team calendar |  TeamCalendar\.Edit  | [Edit published staff schedules in the Published Calendar user experience](scheduling-view-schedule-supervisors.md)\.  | 

## Agent Applications<a name="agentapplications-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Agent application schedule calendar |  StaffCalendar\.View StaffCalendar\.Edit  | [Ability for agents to view their schedules](scheduling-view-schedule-agents.md)\.  | 
| Custom views |  CustomViews\.Access  | Use the [Agent Workspace guided experience](step-by-step-guided-experiences.md) guide\.  | 
| Wisdom \- View |  Wisdom\.View  | [View real\-time recommendations in the agent application](use-realtime-recommendations.md)\.  | 

## Cases<a name="cases-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Cases \- Create |  Cases\.Create  | [Create cases in the agent application](create-cases.md)\.   | 
| Cases \- View |  Cases\.View  | View cases in the agent application\.  | 
| Cases \- Edit |  Cases\.Edit  | Edit cases in the agent application\.  | 
| Case Fields \- Create |  CaseFields\.Create  | [Create case fields](case-fields.md)\.   | 
| Case Fields \- View |  CaseFields\.View  | View case fields\.  | 
| Case Fields \- Edit |  CaseFields\.Edit  | Edit case fields\.  | 
| Case Templates \- Create |  CaseTemplates\.Create  | [Create case templates](case-templates.md)\.   | 
| Case Templates \- View |  CaseTemplates\.View  | View case templates\.  | 
| Case Templates \- Edit |  CaseTemplates\.Edit  | Edit case templates\.  | 

## Campaigns<a name="campaigns-permissions-list"></a>


| UI name | API name | Use | 
| --- | --- | --- | 
| Campaigns \- Create |  Campaigns\.Create  | [Create outbound campaigns](how-to-create-campaigns.md)\.  | 
| Campaigns \- Delete |  Campaigns\.Delete  | Delete outbound campaigns\.  | 
| Campaigns \- Edit |  Campaigns\.Edit  | Edit outbound campaigns\.  | 
| Campaigns \- Manage |  Campaigns\.Delete  | Manage outbound campaigns\.  | 
| Campaigns \- View |     | View outbound campaigns\.  | 