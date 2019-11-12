# Preview: Upcoming Changes to Metrics<a name="upcoming-changes"></a>

Thanks to your feedback, we're making changes to Amazon Connect metrics\. This topic gives you a preview of future improvements\. 

## Real\-Time Metrics: Name Changes for "Missed" and "Agent Status" and "On Call"<a name="upcoming-changes-names"></a>

The following metrics are going to be renamed:


| Old Name | New Name | 
| --- | --- | 
|  Missed  | Agent non\-response  | 
|  Agent Status  | Agent Activity  | 
|  On Call  | On Contact  | 

For each metric, existing saved reports will automatically start displaying the new name; you won't need to do anything for the new name to appear in your reports\. 

The column order for a saved report containing one of these metrics will stay the same\. For example, if you previously saved a report where **Agent Status** was the third metric, then after the update when you open that saved report, **Agent Activity** will be the name for the third metric\.

For **Missed**, only the name of the metric will be changed; the underlying calculation stays the same\. We're changing the name of this metric to **Agent non\-response** so it better reflects its definition: 
+ **Agent non\-response** increments whenever a contact is offered to an agent, and the agent doesn't respond to the contact for whatever reason\. 

  For example, the agent could have intentionally let the timer run out, or the agent could have forgotten to grant microphone access in the Contact Control Panel and never heard the ring\. In these situations, Amazon Connect doesn't drop the contact\. Instead, the routing engine will offer it to another available agent, while the customer continues to wait in queue\. This means a single contact could result in multiple **Agent non\-responses** before an agent responds and handles the contact\.

For **On Call**, the upcoming name change to **On Contact** applies to the Real\-time metrics UI only\. You can continue using `AGENTS_ON_CALL` with the ` GetCurrentMetricData` API to retrieve data for this metric\.

## Label Updates for "Agent Activity" and "Contact State"<a name="upcoming-changes-labels"></a>

Labels are the values returned in a report\. For example, in the following image **Available** and **Basic Routing Profile** are labels\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/labels.png)

For **Agent Activity** and **Contact State**, we're going to rename some of the labels that describe what the agent's current activity is and what's happening with the contact they are currently working on\. This way, the labels in the Real\-Time Metrics report will be more consistent with the labels the agent sees in the Contact Control Panel\. They will also align with the data returned about these different states in other parts of Amazon Connect\.

When the name of **Agent Status** changes to **Agent Activity**, the following labels will change as well:


| Scenario | Before: Agent Status Labels | After: Agent Activity Labels | Notes | 
| --- | --- | --- | --- | 
|  Agent is logged in but offline  |  Not shown  |  Not shown  |   | 
|  Agent switches to **Available** in the CCP  |  Available  |  Available  |   | 
|  Agent has an incoming call  |  CallIncoming  |  Incoming  |  ContactState = Incoming contact  | 
|  Agent has an incoming callback  |  CallbackIncoming  |  Incoming  |  ContactState = Callback incoming  | 
|  Agent accepted a callback, which is now making an outbound call to the customer  |  Calling  |  On Contact  |  ContactState = Callback dialing  | 
|  Agent makes outbound call \(regardless of what status the agent chose in their CCP\)  |  Calling  |  On Contact  |  ContactState = Calling  | 
|  Agent missed a phone call due to timer expired  |  MissedCallAgent  |  Missed  |   | 
|  Agent is interacting with customer on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |   | 
|  Agent puts customer on hold while on phone call \(regardless of what status the agent chose in their CCP\)  |  On call  |  On Contact  |   | 
|  After agent hangs up call  |  After call work  |  After contact work  |   | 
|  Agent is on Lunch \(a custom status\)  |  Lunch  |  Lunch  |   | 
|  Supervisor's activity state if they are monitoring some agent  |  Monitoring  |  Monitoring  |   | 
|  Agent's activity state if they are connected to customer while being monitored by a supervisor  |  On call  |  On Contact  |   | 

The following table shows the how the labels are going to change for **Contact State**\.


| Scenario | Label Name Before | Label Name After | 
| --- | --- | --- | 
|  Agent is logged in but offline  |   |   | 
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