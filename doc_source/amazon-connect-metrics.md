# Amazon Connect Metrics and Contact Trace Records<a name="amazon-connect-metrics"></a>

In Amazon Connect, data about contacts are captured in contact trace records \(CTR\)\. This data can include the amount of time a contact spends in each state: customer on hold, customer in queue, agent interaction time\. 

The basis for most historical and real\-time metrics in Amazon Connect is the data in the CTR\. When you create metrics reports, the values displayed for **most** \(not all\) metrics in the report are calculated using the data in the CTRs\. 

CTRs are available within your instance for 24 months from the time when the associated contact was initiated\. You can also stream CTRs to Amazon Kinesis to retain the data longer, and perform advanced analysis on it\.

**Tip**  
For detailed information about the activity of agents in your contact center, use [Amazon Connect Agent Event Streams](agent-event-streams.md)\.

**Topics**
+ [What's New in Metrics](upcoming-changes.md)
+ [About Agent Status](metrics-agent-status.md)
+ [About Contact States](about-contact-states.md)
+ [Real\-time Metrics Reports](real-time-metrics-reports.md)
+ [Historical Metrics Reports](historical-metrics.md)
+ [Contact Search](contact-search.md)
+ [View a CTR in the UI](sample-ctr.md)
+ [Contact Trace Records Data Model](ctr-data-model.md)