# Amazon Connect feature specifications<a name="feature-limits"></a>

**Note**  
Feature specifications cannot be increased\.

The following table lists Amazon Connect feature specifications\.


| Item | Feature Specification | 
| --- | --- | 
| Agent activity retention  |  24 months from the time the event occurred  | 
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
|  Past chat transcript file size\. This applies to [persistent chat](chat-persistence.md)\.   |  5MB  | 
|  Number of past contacts that can be traversed by Amazon Connect chat\. This applies to [persistent chat](chat-persistence.md)\.   |  100  | 
|  Task templates per instance  |  50  | 
|  Task template customized fields per instance  |  50  | 
|  Maximum duration of a task  |  7 days  | 
|  Maximum number of transfers for a task  |  11 transfers  | 
|  Maximum number of linked tasks on an existing contact  |  11  | 
|  Limit on creating and deleting instances  | 100 instances can be created or deleted in 30 days Amazon Connect enforces a limit on the **total** number of instances that you can create and delete in 30 days\. If you exceed this limit, you will get an error message indicating there has been an excessive number of attempts at creating or deleting instances\. You must wait 30 days before you can restart creating and deleting instances in your account\. For example, if you create 80 instances and delete 20 over the course of 30 days, you must wait an additional 30 days before you can create or delete any more instances\. If you create and delete the same instance 100 times in 30 days, the limit also applies\.   | 

## Forecasting, capacity planning, and scheduling feature specifications<a name="forecasting-cap-planning-scheduling-specs"></a>


| Item | Feature Specification | 
| --- | --- | 
| Agents per schedule |  500  | 
| Agents per staffing group |  75  | 
| Capacity plans per instance |  500  | 
| Capacity scenarios per instance |  500  | 
| Capacity plan user data uploads per instance |  500  | 
| Capacity plan override uploads per instance |  5000  | 
| Concurrent uploads per instance |  20  | 
| File size per upload of capacity plan user data |  1000  | 
| File size per upload of capacity plan overrides |  250  | 
| File size per upload of forecast overrides |  250  | 
| File size per upload of historical actuals |  1000  | 
| Forecast groups per instance |  500  | 
| Forecast override uploads per instance |  500  | 
| Historical actuals uploads per instance |  150  | 
| Queues per forecast group |  200  | 
| Managers per staffing group \(supervisors/schedulers\) |  30  | 
| Schedules per instance |  600  | 
| Shift activities per instance |  300  | 
| Shift activities per shift profile |  10  | 
| Shift profiles per instance |  200  | 
| Staffing groups per instance |  100  | 
| Supervisors per staffing group |  5  | 

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


| Item | Feature Specification | 
| --- | --- | 
| Custom vocabularies |  20  | 
| Contact Lens rules for post\-call |  500  | 
| Contact Lens rules for post\-chat |  500  | 
| Contact Lens rules for real\-time |  500  | 

## Evaluation forms feature specifications<a name="evaluationforms-feature-specs"></a>


| Item | Feature Specification | 
| --- | --- | 
| Maximum number of evaluation forms per instance Historical versions are not counted, only form names are counted\. |  50  | 
| Maximum number of versions per form |  50  | 
| Maximum number of sections per form |  100  | 
| Maximum number of questions per form |  100  | 
| Maximum nesting level of sections |  2 \(sections can have sub\-sections, but sub\-sections cannot have sub\-sub\-sections\)  | 
| Definition title length |  1\-128 characters  | 
| Section title length |  1\-128 characters  | 
| Question title length |  1\-350 characters  | 
| Section instructions length |  up to 1024 characters  | 
| Number of answer options for single select questions |  2\-256 answer options  | 
| Answer option text length for single select questions |  1\-128 characters  | 

## Amazon Connect Rules feature specifications<a name="rules-feature-specs"></a>

The following table lists feature specifications for Amazon Connect Rules\.


| Item | Feature Specification | 
| --- | --- | 
| Conditions in a rule |  20  | 
| Rules per event source type |  500  | 


| Condition type | Number of entries or selections | Post\-call | Post\-chat | Real\-time | 
| --- | --- | --- | --- | --- | 
| Words or phrases \- Exact match |  100  |  Yes  |  Yes  |  Yes  | 
| Words or phrases \- Semantic match |  4  |  Yes  |  Yes  |  Not supported  | 
| Words or phrases \- Pattern match |  100  |  Yes  |  Yes  |  Yes  | 
| Queue condition |  100  |  Yes  |  Yes  |  Yes  | 
| Agent condition |  100  |  Yes  |  Yes  |  Yes  | 
| Custom attributes |  5  |  Yes  |  Yes  |  Yes  | 
| Sentiment \- Time period |  5  |  Yes  |  Yes  |  Yes  | 
| Sentiment \- Entire contact |  5  |  Yes  |  Yes  |  Not supported  | 
| Interruptions |  5  |  Yes  |  Yes  |  Not supported  | 
| Response time |  4 hours  |  Not supported  |  Yes  |  Not supported  | 
| Non\-talk time |  5 hours  |  Yes  |  Not supported  |  Not supported  | 