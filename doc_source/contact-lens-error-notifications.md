# Error notifications: When Contact Lens can't analyze a contact<a name="contact-lens-error-notifications"></a>

It's possible that Contact Lens can't analyze a contact file, even though analysis is enabled on the contact flow\. When this happens, Contact Lens sends error notifications using Amazon EventBridge events\. 

## Subscribe to EventBridge notifications<a name="contact-lens-error-notifications-subscribe"></a>

To subscribe to these notifications, create a custom EventBridge rule that matches the following:
+ "source" = "aws\.connect"
+ "detail\-type" = "Contact Lens Analysis State Change"

The following image shows what this looks like in EventBridge:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-eventbridge-rule.png)

You can also add to the pattern to be notified when a specific event code occurs\. For more information, see [Event Patterns](https://docs.aws.amazon.com/eventbridge/latest/userguide/filtering-examples-structure.html) in the *Amazon EventBridge User Guide*\.

The format of a notification looks like the following sample: 

```
{
    "version": "0", // set by CloudWatch Events
    "id": "55555555-1111-1111-1111-111111111111", // set by CloudWatch Events
    "source": "aws.connect",
    "detail-type": "Contact Lens Analysis State Change",
    "account": "111122223333",
    "time": "2020-04-27T18:43:48Z",
    "region": "us-east-1", // set by CloudWatch Events
    "resources": [
        "arn:aws:connect:us-east-1:111122223333:instance/abcd1234-defg-5678-h9j0-7c822889931e",
        "arn:aws:connect:us-east-1:111122223333:instance/abcd1234-defg-5678-h9j0-7c822889931e/contact/efgh4567-pqrs-5678-t9c0-111111111111"
    ],
    "detail": {
        "instance": "arn:aws:connect:us-east-1:111122223333:instance/abcd1234-defg-5678-h9j0-7c822889931e",
        "contact": "arn:aws:connect:us-east-1:111122223333:instance/abcd1234-defg-5678-h9j0-7c822889931e/contact/efgh4567-pqrs-5678-t9c0-111111111111",
        "channel": "VOICE",
        "state": "FAILED",
        "reasonCode": "RECORDING_FILE_CANNOT_BE_READ"
    }
}
```

## Event codes<a name="contact-lens-event-codes-listed"></a>

 The following table lists the event codes that may result when Contact Lens can't analyze a contact\.


| Event reason code | Description | 
| --- | --- | 
| INVALID\_ANALYSIS\_CONFIGURATION  | Contact Lens received invalid values when the contact flow was initiated, such as an unsupported or invalid language code, or an unsupported value for redaction behavior\.  | 
| RECORDING\_FILE\_CANNOT\_BE\_READ  | Contact Lens can't get the recording file\. This might be because file isn't present in the S3 bucket, or there are problems with permissions\.  | 
| RECORDING\_FILE\_TOO\_SMALL  |  The recording audio file is too small for analysis \(less than 105 ms\)\.  | 
|  RECORDING\_FILE\_TOO\_LARGE  | The recording file exceeds the duration limit for analysis \(more than 14,400 seconds, or 4 hours\)\.  | 
|  RECORDING\_FILE\_INVALID  | The audio file is invalid\.  | 
|  RECORDING\_FILE\_CANNOT\_BE\_READ  | An error occurred when Contact Lens tried to read the audio file\.  | 
|  RECORDING\_FILE\_EMPTY  | The audio file is empty\.  | 
|  RECORDING\_SAMPLE\_RATE\_NOT\_SUPPORTED  | The sample rate of the audio file is not supported\. Contact Lens currently supports audio files with an 8kHz sample rate\. That is the sample rate for Amazon Connect recordings\.  | 