# TransferParticipantToThirdParty<a name="participant-actions-transferparticipanttothirdparty"></a>

Transfers the participant to a specified phone number\. Optionally continues flow running if the third party disconnects while the participant is still connected\. 

## Parameter object<a name="transferparticipanttothirdparty-parameter"></a>

```
{
    "ThirdPartyPhoneNumber": A phone number, in e.164 format, of the external number to which to transfer the contact. May be defined statically or dynamically. 
    "ThirdPartyConnectionTimeLimitSeconds": An integer, between 0 and 600 (inclusive) representing the number of seconds to wait for the third party to answer before canceling the third party call. Only used if ContinueFlowExecution is not False. Must be defined fully statically or as a single valid JSONPath identifier.
    "ContinueFlowExecution": "True" or "False". If not defined or True, the flow continues running after the third party call finishes, if False the flow does not continue, as long as the phone call to the third party succeeds. Must be defined statically. 
    "ThirdPartyDTMFDigits": An optional series of DTMF digits to send to the third party when the call succeeds. Must be defined fully statically or as a single valid JSONPath identifier. Must be 50 or fewer characters chosen from numeric digits, comma, asterisk, and pound sign
    "CallerId": { Optional, an override of the caller ID to present when dialing the third party
        "Number": The caller ID number to present when dialing the third party. Must be defined fully statically or as a single valid JSONPath identifier.
        "Name": The caller ID name to present when dialing the third party. May be defined statically or dynamically.
    }
}
```

## Results and conditions<a name="transferparticipanttothirdparty-results"></a>

None\. Conditions are not supported\.

## Errors<a name="transferparticipanttothirdparty-errors"></a>
+ ConnectionTimeLimitExceeded \- the call has taken longer than the specified time limit to be answered by the third party, and has been canceled\. Supported only when ContinueFlowExecution is True\.
+ CallFailed \- The call was unable to connect successfully\. Only supported when ContinueFlowExecution is True\.
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="transferparticipanttothirdparty-restrictions"></a>

This action is only allowed by the Voice channel\.

This action is allowed in contact flows, transfer flows, and customer queue flows\.

## Corresponding block in the UI<a name="transferparticipanttothirdparty-ui"></a>

[Transfer to phone number](transfer-to-phone-number.md)