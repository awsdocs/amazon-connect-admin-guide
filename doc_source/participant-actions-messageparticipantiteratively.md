# MessageParticipantIteratively<a name="participant-actions-messageparticipantiteratively"></a>

Loops a sequence of prompts while a customer or agent is on hold or in queue\. This block can be configured with an interruption timeout when in a Queue flow that interrupts the message loop to run other flow logic\. The message loop can include entries for both Text and Prompts\. 

## Parameter object<a name="messageparticipantiteratively-parameter"></a>

```
{
   "Messages" : [ A List of messages to be played in a loop. These are defined with either TTS or a Prompt
       {
         "Text" : An optional string that defines text to send to the participant
       },
       {
         "PromptId" : A prompt ID or prompt ARN to play to the participant
       },
       { 
         "SSML" : An optional string that defines the ssml  
       },
       {
         "Media": { An optional object that defines an external media source
           "Uri": Location of the message
           "SourceType": The source from which the message will be fetched. The only supported type is S3
           "MediaType": The type of the message to be played. The only supported type is Audio
         }
       }
       
   ],
   "InterruptFrequencySeconds" : [Optional] Time to elapse before the action completes with "MessagesInterrupted" run result 
}
```

## Results and conditions<a name="messageparticipantiteratively-results"></a>

When the timeout elapses, the action completes with the result as "MessagesInterrupted"\. Conditions are supported, but only the "Equals" operator is supported\. The only supported operand is MessagesInterrupted\.

## Errors<a name="messageparticipantiteratively-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="messageparticipantiteratively-restrictions"></a>

This action is supported in Customer Queue, Customer Hold, and Agent Hold flows\.

"PromptId" is supported only for the Voice channel, all other channels support only the "Text" option\.

If this action is used on the chat channel, it immediately takes the error branch\. If no error branch is available, the flow stop running and the contact is routed to next available agent\. 

## Corresponding block in the UI<a name="messageparticipantiteratively-ui"></a>

[Loop prompts](loop-prompts.md)