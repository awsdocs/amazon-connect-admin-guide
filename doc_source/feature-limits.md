# Amazon Connect feature specifications<a name="feature-limits"></a>

**Note**  
Feature specifications cannot be increased\.

The following table lists Amazon Connect feature specifications\.


| Item | Feature Specification | 
| --- | --- | 
| Maximum size of a real\-time metrics report  |  200KB  | 
| File types supported for chat attachments |  \.csv, \.doc, \.docx, \.jpeg, \.jpg, \.pdf, \.png, \.ppt, \.pptx, \.txt, \.wav, \.xls, \.xlsx   | 
| Max file size for a chat attachment |  20MB  | 
| Attachments per chat conversation |  35  | 
| People who can listen in on the same agent call at the same time  |  5 For example, you can have a group of 5 people listen in to a call at the same time, and then a different group of 5 people listen in to a different call at the same time, and so on\.   | 
| Quick connects you can assign to a queue |  700  | 
| Participants on a conference call |  6 The participants are the customer, agent, and others who can be agents or external third\-parties\.  | 
|  Contact record retention  |  24 months from the time the associated contact was initiated\.  You can choose to stream contact records to Kinesis so you can manage retention and perform advanced analysis\.  | 
|  Max size of the contact record attributes section  |  32KB   | 
|  Active chats per agent  |  10  | 
|  Total duration per chat  |  Up to 7 days, including wait time [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/feature-limits.html)  | 
|  Characters per chat message  |  1024  | 
|  Open websocket connections per chat participant  |  5  | 
|  Chat Amazon Lex bot integration timeout  |  6 seconds The maximum time within which the Amazon Lex bot must respond to the chat customer's prompt\.  | 
|  Task templates per instance  |  50  | 
|  Task template customized fields per instance  |  50  | 
|  Maximum duration of a task  |  7 days  | 
|  Maximum number of transfers for a task  |  11 transfers  | 
|  Maximum number of linked tasks on an existing contact  |  11  | 
|  Limit on creating and deleting instances  | 100 instances can be created or deleted in 30 days Amazon Connect enforces a limit on the **total** number of instances that you can create and delete in 30 days\. If you exceed this limit, you will get an error message indicating there has been an excessive number of attempts at creating or deleting instances\. You must wait 30 days before you can restart creating and deleting instances in your account\. For example, if you create 80 instances and delete 20 over the course of 30 days, you must wait an additional 30 days before you can create or delete any more instances\. If you create and delete the same instance 100 times in 30 days, the limit also applies\.   | 

## Integration association resource feature specifications<a name="integration-association-resource-feature-specs"></a>

The following table lists feature specifications for the integration association resource\. It lists how many of each type of integration association resource can be ingested\.


| Item | Feature Specification | 
| --- | --- | 
| Voice ID domain |  1  | 
| Amazon Pinpoint app |  1  | 
| Event |  10 The event integration resource is used for task triggers\.  | 
| Wisdom assistant |  1  | 
| Wisdom knowledge base |  10  | 
| Cases domain |  1  | 

## Contact Lens for Amazon Connect feature specifications<a name="contact-lens-feature-specs"></a>

The following feature specifications can be changed\. To request changes to the following specifications, use the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.


| Item | Feature Specification | 
| --- | --- | 
| Concurrent real\-time calls with analytics |  50 100 for US East \(N\. Virginia\)  | 
| Concurrent post\-call analytics jobs |  200  See the following [table](#contactlens-concurrent-analytics-jobs) for information about how to derive your concurrent post\-call analytics jobs based on your Amazon Connect call volume\.  | 
| Custom vocabularies |  20  | 
| Contact Lens rules |  200  | 

### Derive Concurrent post\-call analytics jobs based on your Amazon Connect call volume<a name="contactlens-concurrent-analytics-jobs"></a>

A post\-call analytics job is kicked off after the completion of each call with Contact Lens enabled\. The time to complete a post\-call analytics job is about 40% of the call length\. To calculate concurrent post\-call analytics jobs, use the following formula: 

`(average call duration in minutes) * (0.4) * (calls per hour) / (60)`

The following table shows some examples\.


| Average call duration \(in minutes\) | Calls per hour\* | Approximate Concurrent post\-call jobs | 
| --- | --- | --- | 
|  5  |  1000  | 33 | 
|  10  |  500  | 33 | 
|  10  |  1000  | 67 | 
|  10  |  3000  | 200 | 

\*For the calculations in the preceding table, we assume a fairly uniform distribution of calls during the hour\. If you have more complex traffic patterns, [contact AWS Support](https://console.aws.amazon.com/support/home) with details about your anticipated traffic pattern\.

## Amazon Connect Rules feature specifications<a name="rules-feature-specs"></a>

The following table lists feature specifications\.


| Item | Feature Specification | 
| --- | --- | 
| Published rules per instance |  200  | 
| Draft rules per instance |  50  | 
| Conditions in a rule |  20  | 


| Condition type | Number of entries or selections | Post\-call | Real\-time | 
| --- | --- | --- | --- | 
| Words or phrases \- Exact match |  100  |  Yes  |  Yes  | 
| Words or phrases \- Semantic match |  4  |  Yes  |  Not supported  | 
| Words or phrases \- Pattern match |  100  |  Yes  |  Yes  | 
| Queue condition |  100  |  Yes  |  Yes  | 
| Agent condition |  100  |  Yes  |  Yes  | 
| Custom attributes |  5  |  Yes  |  Yes  | 
| Sentiment \- Time period |  5  |  Yes  |  Yes  | 
| Sentiment \- Entire contact |  5  |  Yes  |  Not supported  | 
| Interruptions |  5  |  Yes  |  Not supported  | 
| Non\-talk time |  5  |  Yes  |  Not supported  | 