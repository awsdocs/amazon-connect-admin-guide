# Amazon Connect Metrics and Contact Trace Records<a name="amazon-connect-metrics"></a>

In Amazon Connect, data about contacts, such as the amount of time a contact spends in each state \(customer on hold, customer in queue, agent interaction time\) are captured in contact trace records \(CTR\)\. The basis for most historical and real\-time metrics in Amazon Connect is the data in the CTR\. When you create metrics reports, the values displayed for most metrics in the report are calculated using the data captured in the CTRs\.

Not all metrics are derived from CTR data\.

Within Amazon Connect, you can generate a number of real\-time and historical metric reports to monitor efficiency and utilization, agent performance, and other information about your contact center\. CTRs are available within your instance for 24 months from the time at which the associated contact was initiated\. You can also choose to stream CTRs to Amazon Kinesis so that you can manage retention and perform advanced analysis on the data for your contact center\.

To get detailed information on the activity of agents in your contact center, you can use [Amazon Connect Agent Event Streams](agent-event-streams.md)\.

**Topics**
+ [Real\-time Metrics Reports](real-time-metrics-reports.md)
+ [Historical Metrics Reports](historical-metrics.md)
+ [Contact Trace Records Data Model](ctr-data-model.md)