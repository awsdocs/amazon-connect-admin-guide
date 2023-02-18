# JSONPath Reference for Rules action public API fields that support variable injection<a name="contact-lens-variable-injection"></a>

When you create or manage rules programmatically using Amazon Connect APIs \(such as [CreateRule](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateRule.html) or [UpdateRule](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateRule.html)\), you can specify variables for certain parameters\. The variables are resolved at runtime when the action is triggered, based on the value of the [EventSourceName](https://docs.aws.amazon.com/connect/latest/APIReference/API_RuleTriggerEventSource.html) parameter\. 

For example, let's say you're setting up a task action and you want to add more context\. Following is an example of how you could use variable injections to include the ID of the contact and the ID of the agent in the `Description` field of the task: 
+ Customer is unhappy about the phone call\. A swear word was detected during the conversation with agent `$.ContactLens.PostCall.Agent.AgentId` in the contact `$.ContactLens.PostCall.ContactId`

When the action is triggered, his string would resolve to "Customer is unhappy about the phone call\. A swear word was detected during a conversation with agent 12345678\-1234\-1234\-1234\-EXAMPLEID012 in the contact 87654321\-1234\-1234\-1234\-EXAMPLEID345"

The following table lists each event source, and the JSONPath to use for fields that support variable injection\. 


| EventSourceName | JSONPath Reference | 
| --- | --- | 
|  OnPostCallAnalysisAvailable  |  $\.ContactLens\.PostCall\.ContactId $\.ContactLens\.PostCall\.Agent\.AgentId $\.ContactLens\.PostCall\.Queue\.QueueId  | 
|  OnRealTimeCallAnalysisAvailable  |  $\.ContactLens\.RealTimeCall\.ContactId $\.ContactLens\.RealTimeCall\.Agent\.AgentId $\.ContactLens\.RealTimeCall\.Queue\.QueueId  | 
|  OnPostChatAnalysisAvailable  |  $\.ContactLens\.PostChat\.ContactId $\.ContactLens\.PostChat\.Agent\.AgentId $\.ContactLens\.PostChat\.Queue\.QueueId  | 
|  OnSalesforceCaseCreate  |  $\.ThirdParty\.Salesforce\.CaseCreate\.CaseNumber $\.ThirdParty\.Salesforce\.CaseCreate\.Name $\.ThirdParty\.Salesforce\.CaseCreate\.Email $\.ThirdParty\.Salesforce\.CaseCreate\.Phone $\.ThirdParty\.Salesforce\.CaseCreate\.Company $\.ThirdParty\.Salesforce\.CaseCreate\.Type $\.ThirdParty\.Salesforce\.CaseCreate\.Reason $\.ThirdParty\.Salesforce\.CaseCreate\.Origin $\.ThirdParty\.Salesforce\.CaseCreate\.Subject $\.ThirdParty\.Salesforce\.CaseCreate\.Priority $\.ThirdParty\.Salesforce\.CaseCreate\.CreatedDate $\.ThirdParty\.Salesforce\.CaseCreate\.Description  | 
|  OnZendeskTicketCreate  |  $\.ThirdParty\.Zendesk\.TicketCreate\.Id $\.ThirdParty\.Zendesk\.TicketCreate\.Priority $\.ThirdParty\.Zendesk\.TicketCreate\.CreatedAt  | 
|  OnZendeskTicketStatusUpdate  |  $\.ThirdParty\.Zendesk\.TicketStatusUpdate\.Id $\.ThirdParty\.Zendesk\.TicketStatusUpdate\.Priority $\.ThirdParty\.Zendesk\.TicketStatusUpdate\.CreatedAt  | 