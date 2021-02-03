# UpdateContactTextToSpeechVoice<a name="contact-actions-updatecontacttexttospeechvoice"></a>

Updates the Amazon Polly voice used by text\-to\-speech for voice contacts \(message with text\-to\-speech, or Amazon Lex bots\)\. This defaults to Joanna if this action is never run\. 

## Parameter object<a name="updatecontacttexttospeechvoice-parameter"></a>

```
{
    "TextToSpeechVoice": A string holding the name of an Amazon Polly voice. Must be defined statically. If this is an invalid text to speech voice, text to speech is no longer function for this contact.
    "TextToSpeechEngine": The engine associated with the Amazon Polly voice, if it is a neural voice. Must be defined statically. 
}
```

## Results and conditions<a name="updatecontacttexttospeechvoice-results"></a>

None\.

## Errors<a name="updatecontacttexttospeechvoice-errors"></a>

None\.

## Restrictions<a name="updatecontacttexttospeechvoice-restrictions"></a>

None\. This action is supported in all flow types, and across all channels\. 

## Corresponding block in the UI<a name="updatecontacttexttospeechvoice-ui"></a>

[Set voice](set-voice.md)