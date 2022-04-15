# MessageParticipant<a name="participant-actions-messageparticipant"></a>

Sends a message to the participant\. This is an audio prompt or text\-to\-speech for voice contacts, or a text message for other channels\. 

## Parameter object<a name="messageparticipant-parameter"></a>

```
{
    "PromptId": [Optional] A prompt ID or prompt ARN to play to the participant along with gathering input. May not be specified if Text or SSML is also specified. Must be specified either statically or as a single valid JSONPath identifier.
    "Text":  An optional string that defines text to send to the participant along with gathering input. May not be specified if PromptId or SSML is also specified. May be specified statically or dynamically.
    "SSML": An optional string that defines SSML to send to the participant along with gathering input. May not be specified if Text or PromptId is also specified May be specified statically or dynamically.
    "Media": { An optional object that defines an external media source
        "Uri": Location of the message
        "SourceType": The source from which the message will be fetched. The only supported type is S3
        "MediaType": The type of the message to be played. The only supported type is Audio
    }
}
```

## Results and conditions<a name="messageparticipant-results"></a>

None\. No conditions are supported\.

## Errors<a name="messageparticipant-errors"></a>

NoMatchingError \- If an error occurred and no other error matched\.

## Restrictions<a name="messageparticipant-restrictions"></a>

This action is supported in contact flows, transfer flows, whisper flows, and customer queue flows\. It is not supported in hold flows\.

"PromptId" and "SSML" are only supported for the voice channel\. All other channels support only the "Text" option\.

## Corresponding block in the UI<a name="messageparticipant-ui"></a>

[Play prompt](play.md)