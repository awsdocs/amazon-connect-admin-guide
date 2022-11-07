# Amazon Connect Flow language concepts<a name="flow-language-concepts"></a>

The following terms are used in the Flow language\.

## Contact<a name="flow-language-concepts-contact"></a>

Flows can be run in context of a contact\. In this case, they are referred to as *flows*\.

## Participant<a name="flow-language-concepts-participant"></a>

Flows can additionally be run in a participant context\. This allows participant actions—such as playing prompts or getting customer input—to be run\. Certain types of flows, such as "No participants remaining" disconnect flows and Workitem flows, don't have a participant associated\.

## Action types<a name="flow-language-concepts-action-types"></a>

Flow actions have the following implicit types associated with them\. A type determines when an action is attempted\. 
+ [Contact actions in the Amazon Connect Flow language](contact-actions.md)\. These actions are attempted only when the flow is run in context of a contact\. They generally result in contact data being manipulated in some way\.
+ [Flow control actions in the Amazon Connect Flow language](flow-control-actions.md)\. These actions are used only to determine the path through a flow\. They have no side effects\. Certain data may not be available\. For example, contact data isn't available if the action is determining its path based on contact data\. These actions generally work in every circumstance\.
+ [Interactions in the Amazon Connect Flow language](interactions.md)\. These actions have side effects, but don't require a contact or a participant\. Interactions include actions such as invoking an AWS Lambda function\. They generally work in every circumstance\. 
+ [Participant actions in the Amazon Connect Flow language](participant-actions.md)\. These actions are attempted only when the flow is run in context of a participant\. They generally result in an action that the participant experiences, such as playing a prompt or disconnecting\.