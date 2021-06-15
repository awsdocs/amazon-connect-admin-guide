# About the agent activity audit report<a name="agent-activity-audit-report"></a>

The agent activity audit is like a report version of the [agent event stream](agent-event-streams.md)\. All of the data in this report is also in the agent event stream\.

For example, if there's something in the audit report you want to recreate, or if you want to recreate a different time period, you can do so using the agent event stream\.

Following are the items that may appear on the agent activity audit report and what each one means:
+ **Available**: The agent has set their status in the Contact Control Panel \(CCP\) to **Available**\. Contacts can be routed to them\.
+ **Offline**: The agent has set their status in the Contact Control Panel \(CCP\) to **Offline**\. Contacts can not be routed to them\.
+ \[Customer status\]: The agent has set their status in the Contact Control Panel \(CCP\) to a custom status\. Contacts can not be routed to them\.
+ **Joining Customer**: The state between an inbound contact arriving in the contact flow and routing to the agent\.
+ **Connecting Agent**: The state between an inbound contact being routed to an agent and the agent receiving the contact\.
+ **Connected**: When an inbound contact has been established by the agent choosing **Accept** in their CCP\.
+ **Agent Disconnected**: When the agent doesn't choose **Accept** on the inbound contact in 20 seconds, or they choose **Reject**\.
+ **Calling Customer**: The state before an outbound call is established\.
+ **Telecom issue**: When an outbound call is ended before the call is established\. For example, there was an error with the agent's soft phone connection\.