# Supported channels for contact blocks<a name="block-support-by-channel"></a>

The following table lists all available contact blocks, and whether they support routing a contact through the specified channels\. 


| Block | Voice | Chat | Task | 
| --- | --- | --- | --- | 
| [Call phone number](call-phone-number.md)  | Yes | No \- Error branch | No \- Error branch | 
|  [Change routing priority / age](change-routing-priority.md)   | Yes | No | Yes | 
|  [Check call progress](check-call-progress.md)   | Yes | No \- Error branch | No \- Error branch | 
|  [Check contact attributes](check-contact-attributes.md)   | Yes | Yes | Yes | 
|   [Check hours of operation](check-hours-of-operation.md)  | Yes | Yes | Yes | 
|   [Check queue status](check-queue-status.md)   | Yes | Yes | Yes | 
|   [Check Voice ID](check-voice-id.md)   | Yes | No \- Error branch | No \- Error branch | 
|   [Check staffing](check-staffing.md)   | Yes | Yes | Yes | 
|   [Create task](create-task-block.md)   | Yes | Yes | Yes | 
|   [Customer profiles](customer-profiles-block.md)   | Yes | Yes | Yes | 
|  [Disconnect / hang up](disconnect-hang-up.md)  | Yes | Yes | Yes | 
|   [Distribute by percentage](distribute-by-percentage.md)   | Yes | Yes | Yes | 
|   [End flow / Resume](end-flow-resume.md)   | Yes | Yes | Yes | 
|   [Get customer input](get-customer-input.md)   | Yes | Yes when Amazon Lex is used Otherwise, No \- Error branch | Yes | 
| [Get queue metrics](get-queue-metrics.md) | Yes | Yes | Yes | 
|  [Hold customer or agent](hold-customer-agent.md)  | Yes | No \- Error branch | No \- Error branch | 
|  [Invoke AWS Lambda function](invoke-lambda-function-block.md)  | Yes | Yes | Yes | 
|  [Invoke module ](invoke-module-block.md)  | Yes | Yes | Yes | 
|  [Loop](loop.md)  | Yes | Yes | Yes | 
|  [Loop prompts](loop-prompts.md)  | Yes | No \- Error branch | No \- Error branch | 
|   [Play prompt](play.md)  | Yes | Yes | No \- takes the **Okay** branch, but it has no effect | 
|   [Set callback number](set-callback-number.md)   | Yes | No \- Error branch | No \- Error branch | 
|   [Set contact attributes](set-contact-attributes.md)   | Yes | Yes | Yes | 
|  [Set customer queue flow](set-customer-queue-flow.md)  | Yes | Yes | Yes | 
|   [Set disconnect flow](set-disconnect-flow.md)   | Yes | Yes | Yes | 
|   [Set hold flow](set-hold-flow.md)   | Yes | No \- Error branch | No \- Error branch | 
|   [Set logging behavior](set-logging-behavior.md)   | Yes | Yes | Yes | 
|   [Set recording and analytics behavior](set-recording-behavior.md)  | Yes | Yes | No \- Error branch | 
|   [Set Voice ID](set-voice-id.md)   | Yes | No \- Error branch | No \- Error branch | 
|  [Set voice](set-voice.md)   | Yes | No \- Success branch | No \- Success branch | 
|   [Set whisper flow](set-whisper-flow.md)  | Yes | Yes | Yes | 
|   [Set working queue](set-working-queue.md)   | Yes | Yes | Yes | 
|  [Start media streaming](start-media-streaming.md)  | Yes | No \- Error branch | No \- Error branch | 
|  [Stop media streaming](stop-media-streaming.md)  | Yes | No \- Error branch | No \- Error branch | 
|   [Store customer input](store-customer-input.md)   | Yes | No \- Error branch | No \- Error branch | 
|   [Transfer to agent \(beta\)](transfer-to-agent-block.md)  | Yes | No \- Error branch | No \- Error branch | 
|   [Transfer to flow](transfer-to-flow.md)  | Yes | Yes | Yes | 
|   [Transfer to phone number](transfer-to-phone-number.md)  | Yes | No \- Error branch | No \- Error branch | 
|   [Transfer to queue](transfer-to-queue.md)   | Yes | Yes | Yes | 
|   [Wait](wait.md)  | No \- Error branch | Yes | Yes | 