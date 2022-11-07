# Agent activity audit report<a name="agent-activity-audit-report"></a>

The agent activity audit is like a report version of the [agent event stream](agent-event-streams.md)\. All of the data in this report is also in the agent event stream\.

For example, if there's something in the audit report you want to recreate, or if you want to recreate a different time period, you can do so using the agent event stream\.

## Run the agent activity audit report<a name="access-agent-activity-audit"></a>

For a list of required permissions to perform this procedure, see [Permissions required to view historical metrics reports](htm-permissions.md)\. 

1. Log in to your contact center at https://*instance name*\.my\.connect\.aws/\.

1. Choose **Analytics**, **Historical metrics**, **Agents**, **Agent activity audit**\.

1. Choose the agent login, date, and timezone, and then choose **Generate Report**\.

1. To download the results, choose **Download CSV**\.

## Status definitions<a name="agent-activity-status-definitions"></a>

The following values may appear in the **Status** column on agent activity audit report\. 
+ **Available**: The agent has set their status in the Contact Control Panel \(CCP\) to **Available**\. Contacts can be routed to them\.
+ **Offline**: The agent has set their status in the Contact Control Panel \(CCP\) to **Offline**\. Contacts can not be routed to them\.
+ **Custom status**: The agent has set their status in the Contact Control Panel \(CCP\) to a custom status\. Contacts can not be routed to them\.
+ **Joining Customer**: The state between an inbound contact arriving in the flow and routing to the agent\.
+ **Connecting Agent**: The state between an inbound contact being routed to an agent and the agent receiving the contact\.
+ **Connected**: When an inbound contact has been established by the agent choosing **Accept** in their CCP\.
+ **Busy**: The agent is interacting with a customer\.
+ **Agent Disconnected**: When the agent doesn't choose **Accept** on the inbound contact in 20 seconds, or they choose **Reject**\.
+ **Calling Customer**: The state before an outbound call is established\.
+ **Contact Missed**: When the agent misses a contact\. 
+ **Telecom issue**: When an outbound call is ended before the call is established\. For example, there was an error with the agent's soft phone connection\.

**Note**  
If a status appears in your report but is not listed on this page, it is a custom status created by your organization\. Contact your Amazon Connect admin to learn the definition\.