# Flow control actions in the Amazon Connect Flow language<a name="flow-control-actions"></a>

These actions don't have any side effects and are only used to determine the path through a flow\. Certain data may not be available \(such as contact data, if the action is determining its path based on contact data\)\. These actions generally work in every circumstance\.

A flow control action is an action that:
+ Does not need a contact or a participant to succeed\.
+ Controls the behavior of the flow, by either enabling or disabling flow behavior \(such as logging\) or by choosing a branch when the flow runs\.

**Topics**
+ [CheckHoursOfOperation](flow-control-actions-checkhoursofoperation.md)
+ [CheckMetricData](flow-control-actions-checkmetricdata.md)
+ [CheckOutboundCallStatus](flow-control-actions-checkoutboundcallstatus.md)
+ [CheckVoiceId](flow-control-actions-checkvoiceid.md)
+ [Compare](flow-control-actions-compare.md)
+ [DistributeByPercentage](flow-control-actions-distributebypercentage.md)
+ [EndFlowExecution](flow-control-actions-endflowexecution.md)
+ [GetMetricData](flow-control-actions-getmetricdata.md)
+ [Loop](flow-control-actions-loop.md)
+ [StartVoiceIdStream](flow-control-actions-startvoiceidstream.md)
+ [TransferToFlow](flow-control-actions-transfertoflow.md)
+ [UpdateFlowLoggingBehavior](flow-control-actions-updateflowloggingbehavior.md)
+ [Wait](flow-control-actions-wait.md)