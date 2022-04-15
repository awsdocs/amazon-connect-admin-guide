# GetParticipantInput<a name="participant-actions-getparticipantinput"></a>

Gathers customer input \(a DTMF collection for voice contacts, or an entered string for other channels\)\. There are many optional behaviors after gathering this: encryption, validation, storing to a "LastParticipantInput" section on the flow run data, specifying a custom DTMF terminator for voice contacts and so on\. Details are in the parameter object section\. 

## Parameter object<a name="getparticipantinput-parameter"></a>

```
{
    "PromptId": [Optional] A prompt ID or prompt ARN to play to the participant along with gathering input. May not be specified if Text or SSML is also specified. Must be either statically defined or a single valid JSONPath identifier.
    "Text":  An optional string that defines text to send to the participant along with gathering input. May not be specified if PromptId or SSML is also specified. May be defined statically or dynamically.
    "SSML": An optional string that defines SSML to send to the participant along with gathering input. May not be specified if Text or PromptId is also specified. May be defined statically or dynamically. 
    "Media": { An optional object that defines an external media source
        "Uri": Location of the message
        "SourceType": The source from which the message will be fetched. The only supported type is S3
        "MediaType": The type of the message to be played. The only supported type is Audio
    }
    "InputTimeoutSeconds": The number of seconds to wait for input to be collected before proceeding with a timeout error. For the Voice channel this is the timeout until the *first* DTMF digit is entered. Must be defined statically, and must be a valid integer larger than zero.
    "StoreInput": "True" or "False". Must be statically defined.
    "InputValidation": { An object that defines how to validate customer inputs, required if and only if StoreInput is True
        "PhoneNumberValidation": { Optional, one of the ways to validate inputs, make sure that it's a valid phone number. May not be specified if CustomValidation is specified.
             "NumberFormat": "Local" or "E164". If "Local" is specified, it is validated to be a local number (without the + and the country code), "E164" enforces that the customer input is a fully defined e.164 phone number. Must be defined statically.
             "CountryCode": If the number format is "Local", this must be defined. This is the two letter country code to be associated with the input number when validating. Must be defined statically. 
        }
        "CustomValidation": { Optional, the other way to validate inputs. May not be specified if PhoneNumberValidation is specified.
            "MaximumLength": A number representing the maximum length of the input. Must be defined statically. 
        }
    },
    "InputEncryption": { An optional object that defines how to encrypt the customer input. May only be specified if "CustomValidation" is provided.
        "EncryptionKeyId": The identifier of a key that has been uploaded in the AWS console for the purposes of customer input encryption. May be specified statically or dynamically.
        "Key": The PEM definition of the public key to use to encrypt this data. This key must be signed with the encryption key identified by the EncryptionKeyId. May be specified statically or dynamically. 
    },
    "DTMFConfiguration": { An optional object to override default DTMF behavior for voice calls
        "InputTerminationSequence": Up to five digits to serve as the terminating sequence when gathering DTMF
        "DisableCancelKey": "True" or "False". If "True", the "*" key doesn't cancel gathering DTMF digits.
    }
}
```

## Results and conditions<a name="getparticipantinput-results"></a>

If the "StoreInput" option is "True", there is no run result and conditions are not supported\. If the "StoreInput" option is not defined or is "False", the run result is the participant input, and conditions are supported but only the Equals operator may be used on conditions\. The values being compared must be static and be a single character \- 0\-9 numeric, \*, or \#\.

## Errors<a name="getparticipantinput-errors"></a>
+ NoMatchingCondition \- None of the specified conditions evaluated to true\. Must be defined only if StoreInput is False\.
+ NoMatchingError \- if no other Error matches\. Must always be defined\.
+ InvalidPhoneNumber \- the stored input was not a valid phone number according to the specified PhoneNumberValidation\. Must be defined only if StoreInput is true, and PhoneNumberValidation is specified\.

## Restrictions<a name="getparticipantinput-restrictions"></a>

This action is only supported on the voice channel\.

This action can be used in contact flows, transfer flows, and customer queue flows but not in whisper flows or hold flows\.

## Corresponding block in the UI<a name="getparticipantinput-ui"></a>

[Get customer input](get-customer-input.md)