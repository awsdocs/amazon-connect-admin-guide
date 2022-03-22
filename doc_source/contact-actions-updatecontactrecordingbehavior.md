# UpdateContactRecordingBehavior<a name="contact-actions-updatecontactrecordingbehavior"></a>

Sets contact recording behavior, including analysis behavior and which participants of the contact to record\. 

## Parameter object<a name="updatecontactrecordingbehavior-parameter"></a>

```
{
    "RecordingBehavior": { an object that holds the recording behavior
        "RecordedParticipants": [ ] a list of participants to record, chosen from "Agent" and "Customer". An empty list disables recording. Must be set statically.
    }
    "AnalyticsBehavior": { an object that holds the analytics behavior. Can only be set if the RecordedParticipants contains both Agent and Customer
        "Enabled": either "True" or "False". Must be set statically.
        "AnalyticsLanguage": Must be one of languages supported by Contact Lens post-call analysis. Must be set statically. Use the format xx-XX, for example, en-US for US English.
        "AnalyticsRedactionBehavior": either Enabled or Disabled. Defaults to Disabled if not set. Determines whether to redact sensitive data, such as personal information, in the Contact Lens output file and audio recording.
        "AnalyticsRedactionResults": either "RedactedAndOriginal" or "RedactedOnly". Can be set dynamically. Determines whether the customer gets both the redacted and the original transcripts and audio files, or just the redacted transcripts and audio files.
    }
}
```

For a list of languages supported by Contact Lens post\-call analysis, see [Contact Lens for Amazon Connect](supported-languages.md#supported-languages-contact-lens)\. For the 4\-character language code to use, see [Supported languages](https://docs.aws.amazon.com/transcribe/latest/dg/supported-languages.html) in the *Amazon Transcribe Developer Guide*\.

## Results and conditions<a name="updatecontactrecordingbehavior-results"></a>

None\.

## Errors<a name="updatecontactrecordingbehavior-errors"></a>

None\.

## Restrictions<a name="updatecontactrecordingbehavior-restrictions"></a>

This is supported only in contact flows, transfer flows, outbound whispers, and customer queue flows\. This is not supported in agent/customer whispers or hold flows\. 

Analytics is only supported by the voice channel\.

## Corresponding block in the UI<a name="updatecontactrecordingbehavior-ui"></a>

[Set recording and analytics behavior](set-recording-behavior.md)