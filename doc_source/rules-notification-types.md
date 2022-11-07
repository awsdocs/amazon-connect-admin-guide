# Contact Lens notification types<a name="rules-notification-types"></a>

Contact Lens provides the following notification types:
+ Contact Lens Post Call Rules Matched: An EventBridge event is delivered whenever a Contact Lens rule is matched and has triggered post call\. 

  This event contains useful information about the Contact Lens rule that is triggered including the category assigned, and details of the agent, contact and queue\.
+ Contact Lens Real Time Call Rules Matched: An EventBridge event is delivered whenever a Contact Lens rule is matched and has triggered in real time\. 

  This event contains useful information about the Contact Lens rule that is triggered including the category assigned, and details of the agent, contact and queue\.
+ Contact Lens Analysis State Change: An EventBridge event is delivered when Contact Lens is unable to analyze a contact file\. The event contains the Event Reason Code which provides the details on why it was unable to process the file\.

You can use these notification types in a variety of scenarios\. For example, use Contact Lens analysis State Change events to signal unexpected errors in the processing of a contact file where EventBridge event details can be subsequently stored in a CloudWatch log for additional review, trigger additional workflows, or alert relevant support teams for further investigation\. 

The Contact Lens post\-call and real\-time events enable numerous new use cases such as surfacing and visualization of additional insights, for example:
+ Generate alerts on real\-time customer sentiment drops across all calls
+ Aggregating and reporting on reoccurring issues and topics
+ Measuring the impact of the latest marketing campaign by detecting how many customers referenced it during a call
+ Customizing agent compliance standards for each Region and lines of business, and enrolling agents into additional training where required\.